루트 URL은 http://localhost:8080 처럼 도메인명과 포트 뒤에 아무것도 붙이지 않은 URL을 말한다. 우리는 아직 루트 URL에 대한 매핑을 만들지 않았기 때문에 브라우저에 루트 URL에 접속하면 다음과 같은 404페이지가 나타난다.

![image](https://user-images.githubusercontent.com/74352543/221073921-d0abbfd6-8b32-40c9-b3ed-e00591030e89.png)

이번에는 루트 URL 호출시 404 페이지 대신 질문 목록을 출력하도록 해보자. 다음과 같이 MainContrller를 수정하자.

<pre>
<code>
package com.mysite.sbb;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class MainController {

    @GetMapping("/sbb")
    @ResponseBody
    public String index() {
        return "안녕하세요 sbb에 오신것을 환영합니다.";
    }

    @GetMapping("/")
    public String root() {
        return "redirect:/question/list";
    }
}
</code>
</pre>

root 메서드를 추가하고 / URL을 매핑했다. 리턴 문자열 redirect:/question/list는 /question/list URL로 페이지를 리다이렉트 하라는 명령어이다. 스프링부트는 리다이렉트 또는 포워딩을 다음과 같이 할 수 있다.

* redirect:<URL> - URL로 리다이렉트 (리다이렉트는 완전히 새로운 URL로 요청이 된다.)
* forward:<URL> - URL로 포워드 (포워드는 기존 요청 값들이 유지된 상태로 URL이 전환된다.)

이제 http://localhost:8080 페이지 접속을 하면 root 메서드가 실행되어 질문 목록이 표시되는 것을 확인할 수 있을 것이다.
  
