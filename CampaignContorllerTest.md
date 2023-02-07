
# CampaignControllerTest 코드 리뷰

<pre>
<code>
@SpringBootTest(webEnvironment = WebEnvironment.MOCK)
@AutoConfigureMockMvc
public class CampaignControllerTest {

  ObjectMapper objectMapper =
    new ObjectMapper().registerModule(new JavaTimeModule());

  @Autowired
  private MockMvc mvc;
</code>
</pre>

## @SpringBootTest
### 스프링 부트는 해당 어노테이션을 통해 스프링부트 어플리케이션 테스트에 필요한 거의 모든 의존성 제공한다.
### @SpringBootTest는 통합 테스트를 제공하는 기본적인 스프링 부트 테스트 어노테이션이다.


## webEnvironment = WebEnvironment.MOCK
### 테스트의 웹 환경을 설정하는 속성이며 기본값은 WebEnvironment.MOCK 이다.
### WebEnvironment.MOCK는 실제 서블릿 컨테이너를 띄우지 않고 서블릿 컨테이너를 mocking한 것이 실행된다.
### 여기서 Mock라는 것은 테스트를 위해 실제 객체와 비슷한 객체를 만드는 것을 모킹이라고 한다. 테스트 하려는 객체가 복잡한 의존성을 가지고 있을 때, 모킹한 객체를 이용하면 의존성을 단절시킬 수 있어 쉽게 테스트가 가능하다.
