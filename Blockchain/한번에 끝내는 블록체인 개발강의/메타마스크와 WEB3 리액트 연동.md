
### 메타마스크 

이더리움을 이용하는 댑에 크롬 브라우저로 쉽게 접근 할 수 있는 익스텐션 

### 환경설정

node js 설치후 
```
npm init 한다음 enter계속하여 default 값으로 json 생성 
npm install --save-dev hardhat 으로 하드햇 설치 
```

[[Hardhat]]

---

### 네트워크 설정

#### 메타마스크 거래 임시값 맞춤화 켜기 

하드햇 노드 실행 할때,재시작하면 하드햇 노드의 논스는 0으로 바뀌지만
하지만 메타마스크는 기존의 값을 유지한 채로 남아있기때문에 0으로 맞춰서 유지해야될 필요가 있기때문이다. 개발에 유용함 

#### 로컬 네트워크 설정 

> npx hardhat node로 서버를 열기 

그 다음 아래 이미지 그대로 실행 
![[1703670796061.png]]

그 다음 메타마스크에서 계정 가져오기로 
npx hardhat node 실행하여 나온 private key를 복사 붙여넣기 하여 계정을 가져온다.
그러면 정상적으로 이더 1000이 들어온것을 확인할수있다.(절대 메인넷에서 사용하거나 그런것이 아닌 오로지 테스트용도로 사용해야 한다.)

---
### 초기 frontend 설정 

```
npx create-react-app@latest frontend // frontend 폴더이름
cd frontend 
npm start // 이러면 실행 
```

### create-react-app 

> 이걸 통해서 초기 세팅 이것저것을 쉽게 완료된것을 사용하면 된다.

## WEb3 react 연동 

[[REACT]]

### web3 react provider 

> 이더리움 댑을 개발하는 데 손쉽게 가능하게 해준다.

![[Pasted image 20231227202904.png]]

그림처럼 이더리움 네트워크에서 노드와 소통 할 경우 필요하다 
```
import { Web3Provider} from '@ethersproject/providers';

export function getProvider(provider){

    const web3Provider = new Web3Provider(provider);

    web3Provider.pollingInterval =1000;

    return web3Provider;

}
```
>pollingInterval은 블록체인과의 상호 작용을 주기적으로 수행하는 간격을 밀리초 단위로 정의합니다. 이 예에서는 1000밀리초 또는 1초로 설정되어 있습니다.


#### web3 provider 하위의 useWeb3React로 context 얻을수있다.

