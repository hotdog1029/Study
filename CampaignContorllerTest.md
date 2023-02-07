
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
