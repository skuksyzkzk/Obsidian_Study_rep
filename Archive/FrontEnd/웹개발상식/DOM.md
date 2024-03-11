
# Document Object Model 
사실 우리가 사용하는 document.get~ 이렇게 사용하는 document는 
브라우저에서 제공하는 window객체의 한 요소이다 

**DOM** (Document Object Model) 은 [HTML](https://developer.mozilla.org/ko/docs/Glossary/HTML) 또는 [XML](https://developer.mozilla.org/ko/docs/Glossary/XML) 기반 문서와 상호작용하고 표현하는 [API](https://developer.mozilla.org/ko/docs/Glossary/API)입니다. DOM은 [browser](https://developer.mozilla.org/ko/docs/Glossary/Browser)에서 로드되며, [node](https://developer.mozilla.org/ko/docs/Glossary/Node/DOM) 트리(각 노드는 문서의 부분을 나타냅니다)로 표현하는 문서 모델입니다(
![[Pasted image 20240110193738.png]]

## 순서 

HTML -> 브라우저 -> 파싱 (해석) -> DOM 생성 
![[Pasted image 20240110193907.png]]

이런식의 돔이 생성되는 것
트리형식으로 요소하나가 NODE라고 한다 
