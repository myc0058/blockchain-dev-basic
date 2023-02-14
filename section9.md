# **Section 9 - Presale - Contract** :rocket:

# NewMonkey Contract 만들기

- /contracts/NewMonkey.sol 파일 추가

- NewMonkey.sol 만들기

    - <details><summary>⌨️ Source Code</summary>
    
        ```solidity
        //SPDX-License-Identifier: MIT

        pragma solidity 0.8.17;

        import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
        import "hardhat/console.sol";

        import "@openzeppelin/contracts/access/Ownable.sol";
        import "@openzeppelin/contracts/access/AccessControl.sol";
        import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Enumerable.sol";

        import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
        import "@openzeppelin/contracts/utils/Counters.sol";
        import "@openzeppelin/contracts/utils/Strings.sol";
        import "@openzeppelin/contracts/utils/Base64.sol";

        contract NewMonkey is Ownable, ERC721Enumerable, ERC721URIStorage {
            using Strings for uint256;
            using Counters for Counters.Counter;
            Counters.Counter private _tokenIds;

            mapping(uint256 => uint256) public tokenIdToLevels;
            mapping(uint256 => string) public tokenIdToNames;

            constructor(string memory name, string memory symbol) ERC721(name, symbol) {}

            function getLevels(uint256 tokenId) public view returns (string memory) {
                uint256 levels = tokenIdToLevels[tokenId];
                return levels.toString();
            }

            function generateCharacter(uint256 tokenId) public view returns (string memory) {
                bytes memory svg = abi.encodePacked(
                    '<svg xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMinYMin meet" viewBox="0 0 350 350">',
                    "<style>.base { fill: white; font-family: serif; font-size: 14px; }</style>",
                    '<rect width="100%" height="100%" fill="black" />',
                    '<text x="50%" y="40%" class="base" dominant-baseline="middle" text-anchor="middle">',
                    tokenIdToNames[tokenId],
                    "</text>",
                    '<text x="50%" y="50%" class="base" dominant-baseline="middle" text-anchor="middle">',
                    "Level: ",
                    getLevels(tokenId),
                    "</text>",
                    "</svg>"
                );
                return string(abi.encodePacked("data:image/svg+xml;base64,", Base64.encode(svg)));
            }

            function getTokenURI(uint256 tokenId) public view returns (string memory) {
                bytes memory dataURI = abi.encodePacked(
                    "{",
                    '"name": "Monkey #',
                    tokenId.toString(),
                    '",',
                    '"description": "Monkey created by Mo Young Chul",',
                    '"image": "',
                    generateCharacter(tokenId),
                    '",',
                    '"attributes": [{"trait_type": "Level", "value": ',
                    tokenIdToLevels[tokenId].toString(),
                    " }] ",
                    "}"
                );
                return string(abi.encodePacked("data:application/json;base64,", Base64.encode(dataURI)));
            }

            function mint(string memory name) external onlyOwner {
                _tokenIds.increment();
                uint256 tokenId = _tokenIds.current();
                _safeMint(msg.sender, tokenId);
                tokenIdToLevels[tokenId] = 1;
                tokenIdToNames[tokenId] = name;
                _setTokenURI(tokenId, getTokenURI(tokenId));
            }

            function train(uint256 tokenId) public {
                require(block.number % 2 == 0, "fail train");
                require(_exists(tokenId), "Please use an existing token");
                require(ownerOf(tokenId) == msg.sender, "You must own this token to train it");
                tokenIdToLevels[tokenId] += 1;
                _setTokenURI(tokenId, getTokenURI(tokenId));
            }

            function _beforeTokenTransfer(
                address from,
                address to,
                uint256 firstTokenId,
                uint256 batchSize
            ) internal virtual override(ERC721, ERC721Enumerable) {
                super._beforeTokenTransfer(from, to, firstTokenId, batchSize);
            }

            function supportsInterface(
                bytes4 interfaceId
            ) public view virtual override(ERC721, ERC721Enumerable) returns (bool) {
                return super.supportsInterface(interfaceId);
            }

            function _burn(uint256 tokenId) internal virtual override(ERC721, ERC721URIStorage) {
                super._burn(tokenId);
            }

            function tokenURI(uint256 tokenId) public view virtual override(ERC721, ERC721URIStorage) returns (string memory) {
                return super.tokenURI(tokenId);
            }
        }

        ```
    
    </details>

- modifier는 이미 있는 함수에 기능을 확장할 때 사용합니다. _; 는 modifier 키워드를 붙인 함수의 실행을 뜻하고 _; 위 라인이나 아래 라인에 원하시는 코드를 실행할 수 있게 넣을 수 있습니다. Contract의 bytecode의 사이즈는 제한이 있습니다. modifier를 쓰는 건 bytecode 사이즈를 늘리기 때문에 bytecode의 길이를 줄이는 측면에서는 함수를 호출하는 게 더 좋습니다.

- block은 Contract내에서 어디에서든지 사용할 수 있는 Global 변수입니다. block에 관한 정보들이 들어 있습니다.

- Typechain 만들기
    ```
    npx hardhat typechain
    ```

# NewMonkey NFT UnitTest 만들기

- /test/NewMonkey.test.ts 파일 추가

- NewMonkey.test.ts 만들기

    - <details><summary>⌨️ Source Code</summary>
    
        ```ts
            import { expect } from 'chai';
        import { BigNumber } from 'ethers';
        import { ethers, waffle } from 'hardhat';
        import NewMonkeyArtifact from '../artifacts/contracts/NewMonkey.sol/NewMonkey.json';
        import { NewMonkey } from '../typechain';

        describe('NewMonkey', () => {
            let newMonkey: NewMonkey;

            const [admin, other0, other1, other2, receiver] =
                waffle.provider.getWallets();

            before(async () => {});

            beforeEach(async () => {
                newMonkey = (await waffle.deployContract(admin, NewMonkeyArtifact, [
                'NewMonkey',
                'NMon',
                ])) as NewMonkey;
            });

            it('mint', async () => {
                await newMonkey.mint('brown');
                await newMonkey.mint('james');
                const balance = await newMonkey.balanceOf(admin.address);
                expect(balance).to.be.equal(BigNumber.from(2));
                const totalSupply = await newMonkey.totalSupply();
                expect(totalSupply).to.be.equal(BigNumber.from(2));

                await expect(newMonkey.connect(other0).mint('brown')).to.revertedWith(
                'Ownable: caller is not the owner',
                );
            });

            it('train', async () => {
                await newMonkey.mint('brown');
                const level = await newMonkey.getLevels(1);
                expect(level).to.be.equal(BigNumber.from(1));

                const blockNumber = await ethers.provider.getBlockNumber();
                if (blockNumber % 2 == 0) {
                await ethers.provider.send('evm_mine', []);
                }
                await newMonkey.train(1);

                await expect(newMonkey.train(1)).to.revertedWith('fail train');

                const afterLevel = await newMonkey.getLevels(1);
                expect(afterLevel).to.be.equal(BigNumber.from(2));
            });
        });
        ```
    
    </details>

- Unit Test 실행
    ```
    npx hardhat test .\test\NewMonkey.test.ts
    ```

# Deploy NewMonkey NFT to Klaytn

- /src/new-monkey 폴더 추가

- /src/new-monkey/deploy.ts 파일추가
 
- deploy.ts 스크립트 만들기

    - <details><summary>⌨️ Source Code</summary>
    
        ```ts
        import hre, { ethers } from 'hardhat';
        import NewMonkeyArtifact from '../../artifacts/contracts/NewMonkey.sol/NewMonkey.json';
        import { getGasOption } from '../utils/gas';
        import * as fs from 'fs';

        async function main() {
            const [admin] = await hre.ethers.getSigners();

            const chainId = hre.network.config.chainId || 0;

            const factory = await ethers.getContractFactory(
                NewMonkeyArtifact.contractName,
            );
            const contract = await factory.deploy(
                'NewMonkey',
                'NMon',
                getGasOption(chainId),
            );
            const receipt = await contract.deployTransaction.wait();

            const deployedContract = {
                address: contract.address,
                blockNumber: receipt.blockNumber,
                chainId: hre.network.config.chainId,
                abi: NewMonkeyArtifact.abi,
            };

            const filename = __dirname + `/new-monkey.deployed.json`;

            const deployedContractJson = JSON.stringify(deployedContract, null, 2);
            fs.writeFileSync(filename, deployedContractJson, {
                flag: 'w',
                encoding: 'utf8',
            });

            console.log(deployedContractJson);
        }

        main()
        .then(() => process.exit(0))
        .catch(error => {
            console.error(error);
            process.exit(1);
        });

        ```
    
    </details>

- deploy.ts 실행
    
    ```
    npx hardhat run --network baobab .\src\new-monkey\deploy.ts
    ```

# Mint NewMonkey NFT

- /src/new-monkey/mint.ts 파일추가
 
- mint.ts 스크립트 만들기

    - <details><summary>⌨️ Source Code</summary>
    
        ```ts
        import hre, { ethers } from 'hardhat';
        import { getGasOption } from '../utils/gas';
        import * as fs from 'fs';
        import { NewMonkey } from '../../typechain';

        async function main() {
            const [admin] = await hre.ethers.getSigners();

            const chainId = hre.network.config.chainId || 0;

            const deployedContractJson = fs.readFileSync(
                __dirname + '/new-monkey.deployed.json',
                'utf-8',
            );
            const deployedContract = JSON.parse(deployedContractJson);
            const newMonkey = (await ethers.getContractAt(
                deployedContract.abi,
                deployedContract.address,
            )) as NewMonkey;

            const transaction = await newMonkey.mint('brown', getGasOption(chainId));
            await transaction.wait();
        }

        main()
        .then(() => process.exit(0))
        .catch(error => {
            console.error(error);
            process.exit(1);
        });

        ```
    
    </details>

- mint.ts 실행
    
    ```
    npx hardhat run --network baobab .\src\new-monkey\mint.ts
    ```

- Klaytn scope에서 확인하기

# NewMonkey NFT Train

- /src/new-monkey/train.ts 파일 추가

- train.ts 스크립트 만들기

    - <details><summary>⌨️ Source Code</summary>
    
        ```ts
        import hre, { ethers } from 'hardhat';
        import { getGasOption } from '../utils/gas';
        import * as fs from 'fs';
        import { NewMonkey } from '../../typechain';

        async function main() {
            const [admin] = await hre.ethers.getSigners();

            const chainId = hre.network.config.chainId || 0;

            const deployedContractJson = fs.readFileSync(
                __dirname + '/new-monkey.deployed.json',
                'utf-8',
            );
            const deployedContract = JSON.parse(deployedContractJson);
            const newMonkey = (await ethers.getContractAt(
                deployedContract.abi,
                deployedContract.address,
            )) as NewMonkey;

            const transaction = await newMonkey.train(1, getGasOption(chainId));
            await transaction.wait();
        }

        main()
        .then(() => process.exit(0))
        .catch(error => {
            console.error(error);
            process.exit(1);
        });

        ```
    
    </details>

- train.ts 실행 - 트랜잭션 성공과 실패 두가지 경우 모두 발생시키기

    ```
    npx hardhat run --network baobab .\src\new-monkey\train.ts
    ```

- Klaytn scope에서 확인하기