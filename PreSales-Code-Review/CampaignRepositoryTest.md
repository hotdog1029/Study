# CampaignRepositoryTest 코드 리뷰

# 1.
<pre>
<code>
@DataJpaTest
@AutoConfigureTestDatabase(replace = Replace.NONE)
</code>
</pre>

## @DataJpaTest
@DataJpaTest는 오직 JPA 컴포넌트들만을 테스트하기 위한 어노테이션이다. full-auto config를 해제하고 JPA 테스트와 관련된 config만 적용한다.

## @AutoConfigureTestDatabase
replace=AutoConfigureTestDatabase.Replace가 디폴트로 설정되어 있어, 설정해놓은 DB가 아닌 in-memory DB를 활용해서 테스트가 실행된다.

replace=AutoConfigureTestDatabase.NONE으로 값을 덮어 씌우면 설정해놓은 DB를 테스트에 사용할 수 있다.

## @SpringBootTest
@SpringBootTest는 full application config를 로드해서 통합 테스트를 진행하기 위한 어노테이션이다.


## @Transectional
DB 롤백을 위한 어노테이션

# 2. 
<pre>
<code>
  @Autowired
  private CampaignRepository campaignRepository
</code>
</pre>
필드 인젝션을 해준 모습이다. Test 코드에서는 사용해도 상관없지만 실제 개발 코드에서는 생성자 인젝션을 사용하도록 하자

# 3.
<pre>
<code>
  @Test
  public void create() throws Exception {
    // given
    Campaign campaign = Campaign.builder()
      .name("테스트")
      .purpose("테스트")
      .duration("테스트기간")
      .state("테스트중")
      .budget(0L)
      .cost(0L)
      .product(1)
      .target(1)
      .content(1)
      .channel(1)
      .performance(1)
      .build();

    // when
    campaignRepository.save(campaign);

    // then
    Campaign campaignFind = campaignRepository.findById(campaign.getId())
      .orElseThrow(() -> new Exception("cannot find campaign"));

    assertEquals(campaign, campaignFind);
  }
</code>
</pre>
## @Builder
다수의 필드를 가지는 복잡한 클래스의 경우, 생성자 대신에 빌더를 사용하는 경우가 많다. 빌더 패턴을 직접 작성해보면 코딩량이 의외로 상당함을 깨닫게 된다. 이때 @Builder 어노테이션을 사용하면 자동으로 해당 클래스에 빌더를 추가해주기 때문에 매우 편리하다.

Campaign.builder를 통해 새로운 campaign 생성 => 캠페인리포지토리에 저장 => 생성한 캠페인의 id를 이용해 리포지토리에서 찾음(없으면 예외 발생 구문 추가) => assertEquals를 이용해서 찾은 캠페인과 내가 설정한 캠페인이 같은지 확인

# 4.
<pre>
<code>
  @Test
  public void findAll() throws Exception {
    // given
    List<Campaign> oldCampaignList = campaignRepository.findAll();

    Campaign campaign1 = Campaign.builder()
      .name("테스트1")
      .state("테스트중1")
      .cost(0L)
      .product(1)
      .build();
    campaignRepository.save(campaign1);

    Campaign campaign2 = Campaign.builder()
      .name("테스트2")
      .state("테스트중2")
      .cost(0L)
      .product(2)
      .build();
    campaignRepository.save(campaign2);

    // when
    List<Campaign> newCampaignList = campaignRepository.findAll();

    // then
    assertEquals(newCampaignList.size(), oldCampaignList.size() + 2);
    assertTrue(newCampaignList.contains(campaign1));
    assertTrue(newCampaignList.contains(campaign2));
  }
</code>
</pre>

아무것도 없는 oldCampaignList를 campaignRepository.findAll()을 통해 생성 => 캠페인 1, 캠페인 2를 각각 생성하고 리포지토리에 저장 => 그리고 newCampaignList를 campaignRepository.findAll() 통해 생성 => asswerEquals를 통해 oldCampaignList.size() + 2가 newCampaignList.size()랑 같은지 확인 => newCampaignList에 campaign1,campaign2가 포함되어 있는지 확인

<pre>
<code>
  public void update() throws Exception {
    // given
    Campaign campaign = Campaign.builder()
      .name("테스트")
      .state("테스트중")
      .cost(0L)
      .product(1)
      .build();
    campaignRepository.save(campaign);

    // when
    campaign.setName("새로운테스트");

    // then
    Campaign campaignFind = campaignRepository.findById(campaign.getId())
      .orElseThrow(() -> new Exception("cannot find campaign"));

    assertEquals(campaign.getName(), campaignFind.getName());
  }
</code>
</pre>

새로운 캠페인 생성 => 캠페인 리포지토리에 저장 => setName을 통해 캠페인 이름 다시 설정 => 리포지토리의 캠페인과 내가 설정한 캠페인의 이름이 같은지 확인

<pre>
<code>
  @Test
  public void deleteAll() throws Exception {
    // given
    Campaign campaign1 = Campaign.builder()
      .name("테스트1")
      .state("테스트중1")
      .cost(0L)
      .product(1)
      .build();
    campaignRepository.save(campaign1);

    Campaign campaign2 = Campaign.builder()
      .name("테스트2")
      .state("테스트중2")
      .cost(0L)
      .product(2)
      .build();
    campaignRepository.save(campaign2);

    // when
    campaignRepository.deleteAll();

    // then
    assertTrue(campaignRepository.findAll().isEmpty());
  }
</code>
</pre>

캠페인1, 캠페인2 생성한 후 리포지토리에 저장 => campaignRepository.deleteAll()를 이용하여 모두 삭제 => asserTrue를 이용하여 campaignRepository.findAll()하였을 때 isEmpty 인지확인
