# **Section 11 - Finish** :thumbsup:

# 강의 Review
## Section 1 - 환경설정 :gear:
- Visual Studio 소개
- Node.js 소개
- Visual Studio 설치
- Node.js 설치

## Section 2 - 프로젝트 생성 :gear:
- npm packages 설치
- hardhat.config.ts
- VSCode Extentions 설치
- settings.json, tsconfig.json 파일 추가

## Section 3 - Smart Contract 만들기 :rocket:

- Solidity 소개
- sol 파일 기본구조 소개
- Greeter.sol Compile
- EOA, CA
- eth_call, eth_sendTransaction
- Greeter.sol 진화시키기

## Section 4 - Unit Test 만들기 :yum:
- Unit Test 소개
- Unit Test 기본 구조
- Typechain 파일 만들기
- Greeter.sol Unit Test 만들기

## Section 5 - Smart Contract with Klaytn :spider_web:
- Klaytn network 소개
- EOA 생성
- .env
- hardhat.config.ts
- Deploy Greeter to Klaytn
- Interaction with Smart Contract

## Section 6 - ERC20 :moneybag:
- OpenZeppelin 소개
- ERC20 소개
- ERC20 내 코인 만들기
- Momo Coin UnitTest 만들기
- Deploy Momo Coin to Klaytn
- Momo Coin Balance 가져오기

## Section 7 - ERC721 :monkey_face:
- ERC721 소개
- ERC721 My NFT 만들기
- Monkey NFT UnitTest 만들기
- Deploy Monkey NFT to Klaytn
- Mint Monkey NFT

## Section 8 - Opensea :boat:
- Opensea & Metamask 소개
- Metamask 설치
- Edit My Collection
- Refresh Metadata

## Section 9 - Presale - Contract :rocket:
- NewMonkey Contract 만들기
- NewMonkey NFT UnitTest 만들기
- Deploy NewMonkey NFT to Klaytn
- Mint NewMonkey NFT
- NewMonkey NFT Train

## Section 10 - Presale - Front-End with Metamask :spider_web:
- Web Server(lite-server) 만들기
- Metamask Test 환경 만들기
- Metamask 연동

# 이 강의의 의미

- 이 강의는 저는 블록체인 개발의 Hello world라고 생각하고 있습니다.
- 비 개발자분들에게는 블록체인 개발에 대한 기본적인 지식을 쌓게 해주고 개발자 분들에게는 스스로 학습할 수 있는 기회를 제공할 수 있다고 생각하고 있습니다. 
- 혹시 너무 어렵다고 느끼시거나 난해하다고 느끼신다면 당연한 현상이라고 생각합니다. 이제 첫발을 내 디딘거니까요. :sob:

# 숙제
아래 정보를 이용하여 스스로 mint하여 수료증을 발급받자!!

- Network : Klaytn baobab
- Deployed Contract 정보
  
    <details>
    <summary>basic.certificate.deployed.json</summary>

    ```json
    {
        "address": "0x42183BcD2FD8032F66A4B3eAaaAeA0EB6B16403b",
        "blockNumber": 114280298,
        "chainId": 1001,
        "abi": [
            {
            "inputs": [
                {
                "internalType": "string",
                "name": "name",
                "type": "string"
                },
                {
                "internalType": "string",
                "name": "symbol",
                "type": "string"
                }
            ],
            "stateMutability": "nonpayable",
            "type": "constructor"
            },
            {
            "anonymous": false,
            "inputs": [
                {
                "indexed": true,
                "internalType": "address",
                "name": "owner",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "address",
                "name": "approved",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "Approval",
            "type": "event"
            },
            {
            "anonymous": false,
            "inputs": [
                {
                "indexed": true,
                "internalType": "address",
                "name": "owner",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "address",
                "name": "operator",
                "type": "address"
                },
                {
                "indexed": false,
                "internalType": "bool",
                "name": "approved",
                "type": "bool"
                }
            ],
            "name": "ApprovalForAll",
            "type": "event"
            },
            {
            "anonymous": false,
            "inputs": [
                {
                "indexed": true,
                "internalType": "address",
                "name": "previousOwner",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "address",
                "name": "newOwner",
                "type": "address"
                }
            ],
            "name": "OwnershipTransferred",
            "type": "event"
            },
            {
            "anonymous": false,
            "inputs": [
                {
                "indexed": true,
                "internalType": "address",
                "name": "from",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "address",
                "name": "to",
                "type": "address"
                },
                {
                "indexed": true,
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "Transfer",
            "type": "event"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "to",
                "type": "address"
                },
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "approve",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "owner",
                "type": "address"
                }
            ],
            "name": "balanceOf",
            "outputs": [
                {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "generateCharacter",
            "outputs": [
                {
                "internalType": "string",
                "name": "",
                "type": "string"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "getApproved",
            "outputs": [
                {
                "internalType": "address",
                "name": "",
                "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "owner",
                "type": "address"
                },
                {
                "internalType": "address",
                "name": "operator",
                "type": "address"
                }
            ],
            "name": "isApprovedForAll",
            "outputs": [
                {
                "internalType": "bool",
                "name": "",
                "type": "bool"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "string",
                "name": "name",
                "type": "string"
                }
            ],
            "name": "mint",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [],
            "name": "name",
            "outputs": [
                {
                "internalType": "string",
                "name": "",
                "type": "string"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [],
            "name": "owner",
            "outputs": [
                {
                "internalType": "address",
                "name": "",
                "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "ownerOf",
            "outputs": [
                {
                "internalType": "address",
                "name": "",
                "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [],
            "name": "renounceOwnership",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "from",
                "type": "address"
                },
                {
                "internalType": "address",
                "name": "to",
                "type": "address"
                },
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "safeTransferFrom",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "from",
                "type": "address"
                },
                {
                "internalType": "address",
                "name": "to",
                "type": "address"
                },
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                },
                {
                "internalType": "bytes",
                "name": "data",
                "type": "bytes"
                }
            ],
            "name": "safeTransferFrom",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "operator",
                "type": "address"
                },
                {
                "internalType": "bool",
                "name": "approved",
                "type": "bool"
                }
            ],
            "name": "setApprovalForAll",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "bytes4",
                "name": "interfaceId",
                "type": "bytes4"
                }
            ],
            "name": "supportsInterface",
            "outputs": [
                {
                "internalType": "bool",
                "name": "",
                "type": "bool"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [],
            "name": "symbol",
            "outputs": [
                {
                "internalType": "string",
                "name": "",
                "type": "string"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "index",
                "type": "uint256"
                }
            ],
            "name": "tokenByIndex",
            "outputs": [
                {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
                }
            ],
            "name": "tokenIdToNames",
            "outputs": [
                {
                "internalType": "string",
                "name": "",
                "type": "string"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "owner",
                "type": "address"
                },
                {
                "internalType": "uint256",
                "name": "index",
                "type": "uint256"
                }
            ],
            "name": "tokenOfOwnerByIndex",
            "outputs": [
                {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "tokenURI",
            "outputs": [
                {
                "internalType": "string",
                "name": "",
                "type": "string"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [],
            "name": "totalSupply",
            "outputs": [
                {
                "internalType": "uint256",
                "name": "",
                "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "from",
                "type": "address"
                },
                {
                "internalType": "address",
                "name": "to",
                "type": "address"
                },
                {
                "internalType": "uint256",
                "name": "tokenId",
                "type": "uint256"
                }
            ],
            "name": "transferFrom",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            },
            {
            "inputs": [
                {
                "internalType": "address",
                "name": "newOwner",
                "type": "address"
                }
            ],
            "name": "transferOwnership",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
            }
        ]
    }
    ```

    </details>

- 호출해야할 함수
    
    ```sol
    function mint(string memory name) external {
        ...
    }
    ```

    ```solidity
    function mint(string memory name) external {
        ...
    }
    ```

- mint 함수를 호출하여 수료증 NFT를 수강자님 계정으로 발급받아야 합니다.

- name 파라미터는 본인 이름이나 닉네임을 넣어주세요. (NFT 이미지에 표시 됩니다.)

    ![Alt text](section11/certificate.PNG)

# 다음 강의 계획

- OpenZepplin
    OpenZepplin은 