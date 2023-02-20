# @RequestMapping

우리는 특정 uri로 요청을 보내면 Controller에서 어떠한 방식으로 처리할지 정의를 한다.

이때 들어온 요청을 특정 메서드와 매핑하기 위해 사용하는 것이 @RequestMapping이다.

@RequestMapping에서 가장 많이사용하는 부분은 value와 method이다. (더 많지만 여기서는 여기까지만)

value는 요청받을 url을 설정하게 된다.

method는 어떤 요청으로 받을지 정의하게 된다.(GET, POST, PUT, DELETE 등)

예시를 간단히 들어서 /hello라는 내용으로 GET,POST,PUT,DELETE를 만들려면 어떻게 해야할까?

<pre>
<code>
@RestController
public class HelloController {

    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String helloGet(...) {
        ...
    }

    @RequestMapping(value = "/hello", method = RequestMethod.POST)
    public String helloPost(...) {
        ...
    }

    @RequestMapping(value = "/hello", method = RequestMethod.PUT)
    public String helloPut(...) {
        ...
    }

    @RequestMapping(value = "/hello", method = RequestMethod.DELETE)
    public String helloDelete(...) {
        ...
    }
}
</code>
</pre>

이런식으로 만들 수 있다.

그렇지만 불편하다는 생각이 든다.

이러한 방식을 해결할 수 있는 방식이 있다.

<pre>
<code>
@RestController
@RequestMapping(value = "/hello")
public class HelloController {

    @GetMapping()
    public String helloGet(...) {
        ...
    }

    @PostMapping()
    public String helloPost(...) {
        ...
    }

    @PutMapping()
    public String helloPut(...) {
        ...
    }

    @DeleteMapping()
    public String helloDelete(...) {
        ...
    }
</code>
</pre>

공통적인 url은 class에 @RequestMapping으로 설정해주었다.

그리고 @GetMapping, @PostMapping, @PutMapping, @DeleteMapping으로 간단하게 생략이 가능해졌다.

뒤에 추가적으로 url을 붙이고 싶다면 @GetMapping, @PostMapping, @PutMapping, @DeleteMapping 에 추가적인 url을 작성하면 된다.

<pre>
<code>
@RestController
@RequestMapping(value = "/hello")
public class HelloController {    
    @GetMapping("/hi")
    public String helloGetHi(...) {
        ...
    }
}
</code>
</pre>

위에 있는 helloGethi에 들어가기 위해서는 /hello/hi로 들어가야 한다.
