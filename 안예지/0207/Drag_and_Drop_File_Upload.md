# 모르는 개념 정리

```
1. type 속성
2. FileReader 다시 공부해보기(속성 공부)
3. html <figcaption> 태그
4. Array.from 메서드?
5. dragenter => 파일 안에 들어오면? 기본 이벤트가 뭐길래?(prevent 해주는 거지?)
6. stopPropagation() => 버블링인가 캡쳐링인가(가물가물) 부모 엘리먼트'로'의 이벤트 전달을 막아주는 함수

7. addEventListener의 두번째 인자가 가지는 뜻?(false) 버블링/캡쳐링이랑 연관된 내용인 듯! => 버블링은 자식요소로부터 역행
8. e 객체의 dataTransfer는 무슨 속성일까? 
9. 버블링이 부모 요소로 전파된다는 건 알겠는데, drap&drop 이벤트에서 왜 필요한지는 모르겠음...
```



# DataTransfer

> 드래그앤 드롭 작업 중에 드래그되는 데이터를보유하는 데 사용

- `DataTransfer.files` : 데이터 전송에서 사용할 수 있는 모든 로컬 파일 목록을 포함. 끌기 작업에 파일 끌기가 포함되지 않는 경우 이 속성은 빈 목록이다.



# File

> 파일에 대한 정보를 제공하고, 웹페이지가 JS로 파일의 내용에 접근할 수 있는 방법을 제공하는 <u>객체</u>

- `File.type` : File 객체가 나타내는 파일의 미디어 유형을 반환한다.



# HTML `<figcaption>`

> 부모 `<figure>`요소가 포함하는 다른 컨텐츠에 대한 캡션 설명



# 배열 메서드를 쓸 수 있게 해주는 `Array.from`

> 이터러블이나 유사배열에 배열 메서드를 쓸 수 있도록 해준다. ex) `push`, `pop`

- 인덱스와 `length` 프로퍼티가 있는 *객체*를 유사배열이라고 한다.

- 이터러블은 유사배열과 비슷하지만 `Symbol.iterator`가 구현된 객체(`for...of`를 사용할 수 있다)

- file input이 반환하는 files의 형태 => `FileList`라는 유사배열 객체로 반환된다.

  => 배열 메서드 `forEach()`를 사용 가능하게 할 수 있도록 `Array.from`을 쓴 것으로 보인다.



# 1. HTML

```
```





# 2. CSS

`box-shadow`

> 수평 수직 블러 확산 색상 순서

```css
    box-shadow: 0 1.25em 3.43em rgba(0, 0, 0, 0.08);
/* 수평0 수직 1.25em 흐릿함 3.43 색상 */
```



# 3. JS

## File API

> 파일 API를 사용하면 웹 애플리케이션에서 *파일 및 해당 컨텐츠*에 액세스할 수 있다.
>
> 파일 객체는 `FileReader`객체에 전달되어 파일 내용에 액세스할 수 있다.

- [`FileReader()` 주요 메서드 ](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)

  `.abort()` : 읽기 작업을 중단.

  `.readAsDataURL()` : 파일 데이터를 나타내는 `data:` URL이 `result` 속성에 바인딩

  ```javascript
  FileReader {readyState: 1, result: null, error: null, onloadstart: null, onprogress: null, …}
  error: null
  onabort: null
  onerror: null
  onload: null
  onloadend: null
  onloadstart: null
  onprogress: null
  readyState: 2
  // result 속성 data: URL(이미지 태그의 src)
  result: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIg
  [[Prototype]]: FileReader
  ```

  `.readAsBinaryString()` : 원시 이진 데이터가 문자열로 `result` 속성에 바인딩

  ```javascript
  result: "PNG\r\n\u001a\n\u0000\u0000\u0000\rI..
  ```

  `.readAsText()` : 파일 내용이 텍스트 문자열로 `result` 속성에 포함

  ```javascript
  result: "�PNG\r\n\u001a\n\u0000\u0000\u0000\r..
  ```

  

### fileReader().readAsDataURL()결론

👉 결론 : 가져온 파일의 이미지 src 속성에 값을 바인딩하고 싶으면 fileReader를 `.readAsDataURL` 메서드를 사용해서 파일을 읽어야 한다. 인자로 <u>어떤 파일을 읽을 것인지 전달</u>하는 것도 잊지 않기!



- `onload` 가 이벤트 핸들러면 `addEventListener()`로도 가능한 거 아니야 ? => MDN 문서 가면 이미 명시 돼있더라.

  ```javascript
  addEventListener('loadend', (event) => { });
  
  onloadend = (event) => { };
  ```

  

  - 이벤트 핸들러

  DOM 프로퍼티 `on<Event>` 를 사용하면 핸들러를 할당할 수 있다.

  HTML 속성을 사용해서 할당할 수도 있다.

  > 핸들러를 HTML 속성을 사용해 할당하면 브라우저는 속성값을 이용해 새로운 함수를 만들고 생성된 함수를 DOM의 프로퍼티에 할당한다.

  즉, 두 가지 방법은 동일하게 작동하고, 복수의 이벤트 핸들러를 할당할 수 없다는 공통점을 가지지만 두 가지 방법은 다르다.

  여기서는 DOM 프로퍼티 `on<Event>`로 이벤트핸들러를 할당

  ```javascript
          reader.onloadend = () => {
          let imageContainer =
              document.createElement('figure');}
  
  ```

  `addEventListenter()`로 바꾸면?

  ```javascript
      reader.addEventListener('loadend', () => {
          let imageContainer = document.createElement('figure');
          );
  
  ```

- [자식 노드 모두 삭제하기 `innerHTML`/`textContent`](https://hianna.tistory.com/722)
