# Error Page

- ErrorController 를 구현하는 CustomErrorController 를 만들어 에러에 동적으로 대응할 수 있습니다. 

## Class 소개

- CustomErrorController 예제

ErrorController 를 구현하며 ERROR_STATUS_CODE 에 동적으로 대응할 수 있는 로직을 가지고 있습니다.

```java
@Controller
@RequestMapping("/error")
public class CustomErrorController implements ErrorController {

  private static final String ERROR_PATH = "/error";

  @Override
  public String getErrorPath() {
    return ERROR_PATH;
  }

  @RequestMapping("")
  public String handleError(HttpServletRequest request, Model model) {
    ...
  }
}
```

- ForbiddenException 예제

403 HTTP 에러를 나타내는 클래스 입니다.

```java
@ResponseStatus(value = HttpStatus.FORBIDDEN, reason = "잘못된 접근입니다.")
public class ForbiddenException extends RuntimeException {
}
```

- `throw new ForbiddenException()` 예제
```java
@PutMapping("/{id}")
public String update(@PathVariable long id, User newUser) {
  ...
  throw new ForbiddenException();
  ...
}
```  
## 참고 자료
https://velog.io/@godori/spring-boot-error  
https://supawer0728.github.io/2019/04/04/spring-error-handling/