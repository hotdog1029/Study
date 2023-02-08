# CampaignContorller 코드 리뷰

# 1)

<pre>
<code>
@Tag(name = "Campaign", description = "캠페인 API")
@RestController
@RequestMapping("/campaigns")
@RequiredArgsConstructor
public class CampaignController {

  private final CampaignService campaignService;

  @Tag(name = "Campaign")
  @ApiOperation(value = "캠페인 생성", notes = "입력된 캠페인 정보에 기반하여 새로운 캠페인을 생성합니다.")
  @PostMapping(produces = "application/json")
  @ApiResponse(code = 201, message = "캠페인 생성됨")
  public ResponseEntity<Campaign> addCampaign(@RequestBody AddCampaignDto dto) {
    return new ResponseEntity<>(campaignService.addCampaign(dto),
      HttpStatus.CREATED);
  }

  @Tag(name = "Campaign")
  @ApiOperation(value = "전체 캠페인 조회",
    notes = "DB에 저장된 모든 캠페인을 조회합니다. \n가장 최근에 만들어진 캠페인이 먼저 나타납니다.")
  @GetMapping("/all")
  @ApiResponse(code = 200, message = "전체 캠페인 조회 성공")
  public Iterable<Campaign> getAllCampaigns() {
    return campaignService.getAllCampaigns();
  }

  @Tag(name = "Campaign")
  @ApiOperation(value = "캠페인 조회", notes = "요청된 id에 해당하는 캠페인을 조회합니다.")
  @GetMapping("/{id}")
  @ApiResponse(code = 200, message = "캠페인 조회 성공")
  public Campaign getCampaign(@PathVariable Integer id) {
    return campaignService.getCampaign(id);
  }

  @Tag(name = "Campaign")
  @ApiOperation(value = "캠페인 수정", notes = "요청된 id에 해당하는 캠페인의 내용을 수정합니다.")
  @PutMapping(path = "/{id}", produces = "application/json")
  @ApiResponse(code = 200, message = "캠페인 수정 성공")
  public Campaign setCampaign(@PathVariable Integer id,
    @RequestBody SetCampaignDto dto) {
    return campaignService.setCampaign(id, dto);
  }

  @Tag(name = "Campaign")
  @ApiOperation(value = "캠페인 삭제", notes = "요청된 id에 해당하는 캠페인을 삭제합니다.")
  @DeleteMapping("/{id}")
  @ApiResponse(code = 200, message = "캠페인 삭제 성공")
  public void deleteCampaign(@PathVariable Integer id) {
    campaignService.deleteCampaign(id);
  }
}
</code>
</pre>

# RestController
전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환하기 위해 사용한다. 아래와 같은 과정을 통해 Spring MVC Contanier는 Client의 요청으로부터 View를 반환한다.

하지만 Spring MVC의 컨트롤러를 사용하면서 Data를 반환해야 하는 경우도 있다. 컨트롤러에서는 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용해주어야 한다. 이를 통해 Controller도 Json 형태로 데이터를 반환할 수 있다.

@RestController는 @Controller에 @ResponseBody가 추가된 것이다. 당연하게도 RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것이다. 최근에 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 객체를 ResponseEntity로 감싸서 반환한다.
