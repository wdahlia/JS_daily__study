![password_validation](../assets/password_validation.gif)

# 1. HTML 마크업

```
input 안의 값에 따라 validation 에 있는 리스트에 유효한지 계속 점검
```



# 2. CSS

- `relative`를 써주는 이유가 뭘까?

  

# 3. JS

- 유효성 검사를 어떻게 할까?

  ```
  내 생각 : keyup 이벤트를 쓴다고했으니, keyup 이벤트가 발생할 때마다 input 값을 검사하는데, 소문자, 대문자인 것을 어떻게 판단할 것인가?
  숫자가 들어간 것을 어떻게 검사하는가?
  ```

  => `RegExp`, `regexp.test()` 활용

