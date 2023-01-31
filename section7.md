# **섹션 7 - ERC721** :monkey_face:

- (TODO)

# ERC721 소개

- ERC-721은 증서라고 알려진 NFT의 표준안입니다. NFT는 대체불가토큰(Non Fungible Token)의 약자로 대체 불가능한 토큰이라는 의미이다. 따라서 ERC-721로 발행되는 토큰은 대체 불가능하여 모두 제 각각의 가치(Value)를 갖고 있습니다.

- ERC20(Fungible Token, FT)과 ERC721(Non Fungible Token, NFT)입니다. 보통 FT를 토큰 또는 코인이라고 말하고 NFT와 혼돈될 수 있지만 NFT는 NFT라고 말합니다.

- openzeppelin ERC721폴더를 찾습니다. (/node_modules/@openzeppelin/contracts/token/ERC721)

- IERC721.sol 살펴보기

    - function balanceOf(address owner) external view returns (uint256 balance);

    - function ownerOf(uint256 tokenId) external view returns (address owner);

    - function safeTransferFrom(
        address from,
        address to,
        uint256 tokenId,
        bytes calldata data
    ) external;

    - function safeTransferFrom(
        address from,
        address to,
        uint256 tokenId
    ) external;

    - function transferFrom(
        address from,
        address to,
        uint256 tokenId
    ) external;

    - function approve(address to, uint256 tokenId) external;

    - function setApprovalForAll(address operator, bool _approved) external;

    - function getApproved(uint256 tokenId) external view returns (address operator);

    - function isApprovedForAll(address owner, address operator) external view returns (bool);

- IERC721.sol 살펴보기

# ERC721 내 NFT 만들기

- /contracts/Monkey.sol 파일 추가

- Momo.sol 스크립트 만들기

- Compile
```
npx hardhat compile
```

- Typechain
```
npx hardhat typechain
```

# Monkey NFT UnitTest 만들기

- /test/Monkey.test.ts 파일 추가

- Monkey.test.test 스크립트 만들기

- Unit Test 실행
```
npx hardhat test .\test\Monkey.test.ts
```

# Monkey NFT klaytn에 Deploy

- /src/Monkey 폴더추가

- /src/Monkey/deploy.ts 파일 추가

- deploy.ts 스크립트 만들기

- deploy.ts 실행
```
npx hardhat run --network baobab .\src\Monkey\deploy.ts
```

# Monkey NFT Mint

- /src/Monkey/mint.ts 파일 추가

- mint.ts 스크립트 만들기

- mint.ts 실행
```
npx hardhat run --network baobab .\src\Monkey\mint.ts
```

