# **섹션 9 - Presale - Contract** :rocket:

(TODO)
  
# NewMonkey Contract 만들기

- /contracts/NewMonkey.sol 파일 추가

- NewMonkey.sol 만들기

    ```
    (TODO)
    ```

- modifier는 이미 있는 함수에 기능을 확장할때 사용합니다. _; 는 modifier 키워드를 붙인 함수의 실행를 뜻하고 _; 위 라인이나 아래 라인에 원하시는 코드를 실행할수 있게 넣을수 있습니다. Contract의 bytecode의 사이즈는 제한이 있습니다. modifier를 쓰는건 bytecode 사이즈를 늘리기 때문에 bytecode의 길이를 줄이는 측면에서는 함수를 호출하는게 더 좋습니다.

- block은 Contract내에서 어디에서든지 사용할 수 있는 Global 변수입니다. block에 관한 정보들이 들어 있습니다.

- Typechain 만들기
    ```
    npx hardhat typechain
    ```

# NewMonkey NFT UnitTest 만들기

- /test/NewMonkey.test.ts 파일 추가

- NewMonkey.test.ts 만들기

    ```
    (TODO)
    ```

- Unit Test 실행
    ```
    npx hardhat test .\test\NewMonkey.test.ts
    ```

# NewMonkey NFT klaytn에 Deploy

- /src/new-monkey 폴더 추가

- /src/new-monkey/deploy.ts 파일추가
 
- deploy.ts 스크립트 만들기

    ```
    (TODO)
    ```

- deploy.ts 실행
    
    ```
    npx hardhat run --network baobab .\src\new-monkey\deploy.ts
    ```

# NewMonkey NFT Mint

- /src/new-monkey/mint.ts 파일추가
 
- mint.ts 스크립트 만들기

    ```
    (TODO)
    ```

- mint.ts 실행
    
    ```
    npx hardhat run --network baobab .\src\new-monkey\mint.ts
    ```

- Klaytn scope에서 확인하기

# NewMonkey NFT Train

- /src/new-monkey/train.ts 파일 추가

- train.ts 스크립트 만들기

    ```
    (TODO)
    ```

- train.ts 실행 - 트랜잭션 성공과 실패 두가지 경우 모두 발생시키기

    ```
    npx hardhat run --network baobab .\src\new-monkey\train.ts
    ```

- Klaytn scope에서 확인하기