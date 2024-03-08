
이더리움 개발을 위한 다양한 유틸리티를 포함하는 개발환경
디버깅,배포,테스트 등 여러가지

실행
```
npx hardhat 

//compile and test
npx hardhat compile 
npx hardhat test 

```

초기에 

> npx hardhat 실행후 
> 첫번째 javascript 선택한다음 전부 기본값으로 enter 입력 

기본적으로 contracts,scripts,test 폴더로 이루어진 구조 (js선택하고 설치 완료되면 3개의 폴더가 있을거다.)

> npx hardhat compile 하면 artifacts 폴더의 contracts에 해당 컨트랙트파일의 중요한 json 생성된다.


---

## 로컬 노드 실행 

> yarn hardhat node 
> 테스트로 사용 할 수있는 주소와 개인키를 알수있다 .
> 이걸로 메인넷에서 사용은 안되고, 테스트로만 사용 이더가지고 있음 

노드가 돌아가면서 노드와 테스트로 통신이 가능해진다 .

