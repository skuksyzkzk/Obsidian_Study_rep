웹 스토리지 객체(web storage object)인 `localStorage`와 `sessionStorage`는 브라우저 내에 키-값 쌍을 저장할 수 있게 해줍니다.

이 둘을 사용하면 페이지를 새로 고침하고(`sessionStorage`의 경우) 심지어 브라우저를 다시 실행해도(`localStorage`의 경우) 데이터가 사라지지 않고 남아있습니다. 이 부분은 조만간 뒤에서 살펴보기로 합시다.

# local storage 페이지를 닫았다가 다시 켜도 유지 
# session storage는 페이지 닫으면 끝 

그런데 "쿠키를 사용하면 브라우저에 데이터를 저장할 수 있는데, 왜 또 다른 객체를 사용해 데이터를 저장하는 걸까요?"라는 의문이 들 수 있습니다. 쿠키 이외에도 다른 방식을 사용하는 이유는 다음과 같습니다.

- 쿠키와 다르게 웹 스토리지 객체는 네트워크 요청 시 서버로 전송되지 않습니다. 이런 특징 때문에 쿠키보다 더 많은 자료를 보관할 수 있습니다. 대부분의 브라우저가 최소 2MB 혹은 그 이상의 웹 스토리지 객체를 저장할 수 있도록 해줍니다. 또한 개발자는 브라우저 내 웹 스토리지 구성 방식을 설정할 수 있습니다.
- 쿠키와 또 다른 점은 서버가 HTTP 헤더를 통해 스토리지 객체를 조작할 수 없다는 것입니다. 웹 스토리지 객체 조작은 모두 자바스크립트 내에서 수행됩니다.
- 웹 스토리지 객체는 도메인·프로토콜·포트로 정의되는 오리진(origin)에 묶여있습니다. 따라서 프로토콜과 서브 도메인이 다르면 데이터에 접근할 수 없습니다.

두 스토리지 객체는 동일한 메서드와 프로퍼티를 제공합니다.

- `setItem(key, value)` – 키-값 쌍을 보관합니다.
- `getItem(key)` – 키에 해당하는 값을 받아옵니다.
- `removeItem(key)` – 키와 해당 값을 삭제합니다.
- `clear()` – 모든 것을 삭제합니다.
- `key(index)` – 인덱스(`index`)에 해당하는 키를 받아옵니다.
- `length` – 저장된 항목의 개수를 얻습니다.

두 스토리지 객체는 `Map`과 유사합니다. `setItem/getItem/removeItem`을 지원하죠. 하지만 인덱스를 사용해 키에 접근할 수 있다는 점(`key(index)`)에서 차이가 있습니다.

이제 본격적으로 localStorage와 sessionStorage가 어떻게 동작하는지 살펴봅시다.

## [키 순회하기](https://ko.javascript.info/localstorage#ref-1140)


`localStorage`는 '키’를 사용해 값을 얻고, 설정하고, 삭제할 수 있게 해줍니다. 그렇다면 키나 값 전체는 어떻게 얻을 수 있을까요?

아쉽게도 스토리지 객체는 iterable 객체가 아닙니다.

대신 배열처럼 다루면 전체 키-값을 얻을 수 있습니다.

```
for(let i=0; i<localStorage.length; i++) {

    let key = localStorage.key(i);

    alert(`${key}: ${localStorage.getItem(key)}`);

  }
```



일반 객체를 다룰 때처럼 `for key in localStorage` 반복문을 사용해도 전체 키-값을 얻을 수 있습니다.

하지만 이 방법을 사용하면 필요하지 않은 내장 필드까지 출력됩니다.

## [문자열만 사용](https://ko.javascript.info/localstorage#ref-1141)

`localStorage`의 키와 값은 반드시 문자열이어야 합니다.

숫자나 객체 등 다른 자료형을 사용하게 되면 문자열로 자동 변환됩니다.


# [sessionStorage](https://ko.javascript.info/localstorage#ref-1142)

`sessionStorage` 객체는 `localStorage`에 비해 자주 사용되진 않습니다.

제공하는 프로퍼티와 메서드는 같지만, 훨씬 제한적이기 때문입니다.

- `sessionStorage`는 현재 떠 있는 탭 내에서만 유지됩니다.
    - 같은 페이지라도 다른 탭에 있으면 다른 곳에 저장되기 때문입니다.
    - 그런데 하나의 탭에 여러 개의 iframe이 있는 경우엔 동일한 오리진에서 왔다고 취급되기 때문에 `sessionStorage`가 공유됩니다.
- 페이지를 새로 고침할 때 `sessionStorage`에 저장된 데이터는 사라지지 않습니다. 하지만 탭을 닫고 새로 열 때는 사라집니다.