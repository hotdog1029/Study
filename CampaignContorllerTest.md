
# CampaignControllerTest 코드 리뷰

# 1
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
스프링 부트는 해당 어노테이션을 통해 스프링부트 어플리케이션 테스트에 필요한 거의 모든 의존성 제공한다.

@SpringBootTest는 통합 테스트를 제공하는 기본적인 스프링 부트 테스트 어노테이션이다.

## webEnvironment = WebEnvironment.MOCK
테스트의 웹 환경을 설정하는 속성이며 기본값은 WebEnvironment.MOCK 이다.

WebEnvironment.MOCK는 실제 서블릿 컨테이너를 띄우지 않고 서블릿 컨테이너를 mocking한 것이 실행된다.

여기서 Mock라는 것은 테스트를 위해 실제 객체와 비슷한 객체를 만드는 것을 모킹이라고 한다. 테스트 하려는 객체가 복잡한 의존성을 가지고 있을 때, 모킹한 객체를 이용하면 의존성을 단절시킬 수 있어 쉽게 테스트가 가능하다.

## ObjectMapper
JSON 형식을 사용할 때, 자바 객체를 JSON으로 직렬화하고 요청들을 역직렬화 할 때 사용하는 기술이다.

## JSON(Javascript Object Notation)
"키:값"쌍으로 이루어진 데이터 객체를 전달하기 위해 사람이 읽을 수 있는 텍스트를 사용하는 포맷이다.

## 직렬화(Serialize)
데이터를 전송하거나 저장할 때 바이트 문자열이어야 하기 때문에 객체들을 문자열로 바꾸어 주는 것
Object -> String 문자열

## ObjectMapper objectMapper = new ObjectMapper().registerModule(new JavaTimeModule());
자바의 LocalDateTime을 직렬화 혹은 역직렬화하기 위한 모습

## @Autowired private MockMvc mvc;
실제 객체와 비슷하지만 테스트에 필요한 기능만 가지는 가짜 객체를 만들어서 애플리케이션 서버에 배포하지 않고도 스프링 MVC 동작을 재현할 수 있는 MockMvc 선언

# 2

<pre>
<code>
  @Transactional
  @Test
  public void add() throws Exception {
    String content = objectMapper.writeValueAsString(new AddCampaignDto(
      "이름",
      "목표",
      "실행기간",
      0L,
      1));

    mvc.perform(post("/campaigns").header("Content-Type", "application/json")
      .content(content)).andDo(print())

      .andExpect(status().isCreated()).andExpect(jsonPath("$.name", is("이름")))
      .andExpect(jsonPath("$.purpose", is("목표")))
      .andExpect(jsonPath("$.duration", is("실행기간")))
      .andExpect(jsonPath("$.budget", is(0)))
      .andExpect(jsonPath("$.product", is(1)));
</code>
</pre>

## @Transactioal
DB에 접근하기 위해서 트랜젹은 필수, 데이터 수정 과정에서 성공하면 전체가 성공(commit)해야하고, 실패하면 전체가 실패(RollBack)해주는 트랜잭션을 사용하기 위한 어노테이션

## String content = objectMapper.writeValueAsString(new AddCampaignDto("이름","목표","실행기간",0L,1));
객체를 문자열로 직렬화 해준 모습

## mvc.perform(post("/campaigns").header("Content-Type", "application/json").content(content)).andDo(print())
perform()메소드는 DispatcherServlet에 요청을 의뢰하는 역할을 한다. MockMvcRequestBuilder클래스를 사용해 설정한 요청 데이터를 perform()의 인수로 전달한다.

## .andExpect(status().isCreated()).andExpect(jsonPath("$.name", is("이름"))) ....
andExpect()메소드는 인수에 실행결과를 검증하는 MockMvcResultMatchers에서 제공하는 ResultMatcher 을 지정한다

## 캠페인 추가가 잘되냐 안되냐 확인

# 3

<pre>
<code>
  @Test
  public void add_error() throws Exception {

    assertThrows(Exception.class, () -> {
      mvc.perform(post("/campaigns").header("Content-Type", "application/json")
        .content("{\"name\":\"이름\"}"));
    });

    assertThrows(Exception.class, () -> {
      mvc.perform(post("/campaigns").header("Content-Type", "application/json")
        .content("{\"state\":\"진행상태\"}"));
    });
  }
</code>
</pre>

# 4
## add_error 테스트는 content로 응답 본문 내용 검증을 하는데 {"name":"이름","purpose":"목표","duration":"실행기간","budget":0,"product":1}이 안들어왔으니 예외가 발생
## 캠페인을 추가할 떄 필수 인자값을 안넣으면 오류가 잘나냐 안나냐 확인

<pre>
<code>
  public void all() throws Exception {
    mvc.perform(get("/campaigns/all")).andDo(print())

      .andExpect(status().isOk()).andExpect(jsonPath("$").isArray());
</code>
</pre>

## 모르겠음 // 모든 데이터를 잘 가져오냐 안가져오냐의 테스트인거같음

# 5
<pre>
<code>
  @Transactional
  @Test
  public void id() throws Exception {
    String content = objectMapper
      .writeValueAsString(new AddCampaignDto(
        "이름",
        "목표",
        "실행기간",
        0L,
        1));

    MvcResult result = mvc
      .perform(post("/campaigns").header("Content-Type", "application/json")
        .content(content))
      .andDo(print())

      .andExpect(status().isCreated()).andReturn();

    Campaign campaign = objectMapper
      .readValue(result.getResponse().getContentAsString(), Campaign.class);

    mvc.perform(get("/campaigns/" + campaign.getId())).andDo(print())

      .andExpect(status().isOk()).andExpect(jsonPath("$.name", is("이름")))
      .andExpect(jsonPath("$.purpose", is("목표")))
      .andExpect(jsonPath("$.duration", is("실행기간")))
      .andExpect(jsonPath("$.budget", is(0)))
      .andExpect(jsonPath("$.product", is(1)));
  }
</code>
</pre>
## 캠페인 객체를 생성 => 객체를 String으로 직렬호 => 응답값 mvcResult를 얻어서 다시 오브젝트로 역직렬화 => getId를 통해 해당 Id의 값들과 내가 설정한 값들이 맞는지 확인
