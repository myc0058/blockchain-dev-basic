# **섹션 6 - ERC20** :moneybag:

- (TODO)

# OpenZeppelin 소개

- OpenZeppelin은 블록체인 및 소프트웨어 개발 회사입니다. 또한 이 회사에서 만든 Smart Contract 표준 프레임웍입니다. 보통 OpenZeppelin을 말하면 이 표준 프레임웍을 얘기합니다. 유용한 Smart Contract들의 모음이라고 생각하시면 됩니다.

- OpenZepplin은 보안감사(Audit)를 거쳐 코드의 무결성이 검증되어있습니다. 여러분들이 만든 ERC20 코인을 거래소에 상장할때 Audit은 필수입니다.

- 내가 원하는 기능을 구현하기에 좋은 자료가 되기도 합니다.

- 구글링을 하시면 많은 컨트랙트들이 Github에 오픈되어 있습니다. 개발하시기 전에 참조하시면 많은 도움이 되실거라 생각합니다.


# ERC20 소개

- ERC-20은 Ethereum Request for Comment 20의 약자입니다. 20은 리퀘스트 숫자다. 이더리움 네트워크의 개선안을 제안하는 EIPs(Ethereum Improvement Proposals)에서 관리하는 공식 프로토콜(규약)입니다.

- ERC20 규약을 지켜야 내가 만튼 코인이 널리 사용될수 있습니다. (예 : MetaMask 코인전송)
  
- openzeppelin ERC20폴더를 찾습니다. (/node_modules/@openzeppelin/contracts/token/ERC20)

- IERC20.sol 살펴보기

    - Contract를 상속받으면 하위 Contract(상속받은 Contract)는 상위 Contract의 모든 변수와 함수를 가지게 됩니다.
  
    - 새로운 키워드 internal, external은 private, public과 유사합니다. 다만 internal은 Contract 내부와 하위 Contract에서 호출이 가능하고 external은 Contract 내부에서는 호출할 수 없고 외부에서만 호출이 가능합니다.
  
    - function totalSupply() external view returns (uint256);
        - 총 유통량

    - function balanceOf(address account) external view returns (uint256);
        - 특정 유저의 잔액
  
    - function transfer(address to, uint256 amount) external returns (bool);
        - 내 코인 전송

    - function allowance(address owner, address spender) external view returns (uint256);
        - spender에게 허가된 apporve 총량

    - function approve(address spender, uint256 amount) external returns (bool);
        - spender에게 원하는 양만큼 허가
        - approve 함수를 호출할때 역시 가스비를 지불해야 하기 때문에 편의상 아주 큰 수를 서비스를 처음 이용할때 한번만 approve하곤 합니다.
        
    - function transferFrom(address from, address to, uint256 amount) external returns (bool);
        - 다른 계정의 코인 전송

- ERC20.sol 살펴 보기
  
# ERC20 내 코인 만들기

- /contracts/Momo.sol 파일 추가

- Momo.sol 스크립트 만들기

- Compile
    ```
    npx hardhat compile
    ```

- hardhat.config.ts에 hardhat-typechain import 추가
    ```
    import 'hardhat-typechain';
    ```

- Typechain
    ```
    npx hardhat typechain
    ```

# Momo Token UnitTest 만들기

- hardhat.config.ts에 hardhatwaffle import 추가
    ```
    import '@nomiclabs/hardhat-waffle';
    ```

- /test/Momo.test.ts 파일 추가

- Momo.test.test 스크립트 만들기

- Unit Test 실행
    ```
    npx hardhat test .\test\momo.test.ts
    ```

# Momo Token klaytn에 Deploy

- /src/momo 폴더추가

- /src/momo/deploy.ts 파일 추가

- deploy.ts 스크립트 만들기

- deploy.ts 실행
    ```
    npx hardhat run --network baobab .\src\momo\deploy.ts
    ```


# Momo Token Balance 가져오기

- /src/momo/get-balance.ts 파일 추가

- get-balance.ts 스크립트 만들기

- get-balance.ts 실행
    ```
    npx hardhat run --network baobab .\src\momo\get-balance.ts
    ```