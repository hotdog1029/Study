
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

