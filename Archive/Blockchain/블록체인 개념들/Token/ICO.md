
# initial Coin Offering 

새로운 암호화폐 프로젝트나 블록체인 기반 프로젝트가 자금을 모으기 위해 사용되는 방법 중 하나입니다. ICO는 기업이 자체 암호화폐 토큰을 발행하고 판매함으로써 자금을 조달하는 프로세스를 의미합니다.

ICO는 기업이 자금을 마련하고 프로젝트를 개발하기 위해 투자자들로부터 자금을 모으는 방법으로 사용됩니다. 일반적으로 이러한 ICO에서는 이더리움 블록체인과 스마트 컨트랙트를 기반으로 한 토큰이 발행되며, 이 토큰을 투자자들이 구매할 수 있습니다. 이더리움 블록체인에서 사용되는 대표적인 토큰 표준 중 하나가 ERC-20입니다.

ERC-20은 이더리움 블록체인에서 토큰을 정의하기 위한 표준입니다. 이 표준을 따르는 토큰은 이더리움 네트워크 상에서 상호 운용성을 가지게 됩니다. 따라서 많은 ICO 프로젝트들이 ERC-20 토큰을 발행하여 이더리움 블록체인을 기반으로 ICO를 진행하게 됩니다.

ICO의 성공 여부는 프로젝트의 가치 및 투자자들의 신뢰와 관련이 있습니다. 하지만 ICO에는 투자의 위험이 따르며, 투자자들은 프로젝트를 신중하게 검토하고 투자 결정을 내리는 것이 중요합니다. ICO의 성공 여부와 투자의 수익은 암호화폐 시장의 변동성, 기술적인 성숙도, 팀의 역량 등 여러 요인에 의해 영향을 받을 수 있습니다.

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

  

contract ERC20 {

    mapping(address => uint) private _balances;

    mapping(address => mapping(address=>uint)) private _allowance;

    uint private _totalSupply ; // 대부분 토큰 발행시 MAx값을 정해놓고 시작 그걸 백서에 명시해야된다.

    string private _name;

    string private _symbol;

    uint8 private _decimals;

  

    // burn 은 2가지 경우 존재 user가 하는 경우 관리자가 하는경우

    // burn 으로 유통량 조절

  

    //1.관리자

    function burn(address _to,uint _amount) public {

        _balances[_to] -= _amount;

        _totalSupply -= _amount;

    }

    //2. 스스로

    function burnByuser(uint _amount) public {

        //transfer(address(0),_amount);

        _totalSupply -= _amount;

    }

  

    /*

        ICO를 하다 보면 해킹문제가 발생해서 벤을 해야되는 경우가 발생한다

        블랙 리스트 관리

    */

  

    mapping (address=>bool) private _blackList;

    address public owner ;

  

    constructor() {

        owner = msg.sender;

    }

    modifier checkBlackList() {

        require(!_blackList[msg.sender],"Ban User");

        _;

    }

  

    function setBlackList(address to) public {

        require(owner==msg.sender,"Only admin");//관리자만 설정가능하게 하기 위해서

        _blackList[to] = true;

    }

}
```