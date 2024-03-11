
Web3.eth 와 We3.utils 를 제일 많이 사용 
[[Ethers.js]]도 많이 사용하긴함 

### 주요 메서드 

#### web3.eth.getBalance(address,[,default Block],[,callback])

address 주소의 잔액을 확인한다 callback으로 에러처리 Promise를 반환해준다.
balance 는 wei 단위로 불러옴 

#### web3.eth.getBlock(blockHash or blockNumber,)

블록의 해쉬나 넘버와 매칭된 블록의 정보를 가져온다 

#### web3.eth.getTranscation(transcationHash)

트랜잭션 해쉬에 맞는 트랜잭션 가져옴 가스의 비용등 트랜잭션과 관련된 부분 가져온다 

> send과 call 구분 잘하기


#### web3.utils.sha3() 

해싱해주는 메소드 

web3.utils.isAddress()

이더리움 주소가 맞는지 확인




## Web3 -react 에서 