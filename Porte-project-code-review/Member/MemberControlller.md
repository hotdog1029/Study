<pre>
<code>
@Tag(name = "Member", description = "멤버 API")
@RestController
@RequestMapping("/members")
@RequiredArgsConstructor
public class MemberController {
  private final MemberService memberService;

  @Tag(name = "Member")
  @ApiOperation(value = "멤버 생성", notes = "입력된 멤버 정보에 기반하여 새로운 멤버를 생성합니다.")
  @PostMapping(produces = "application/json")
  @ApiResponse(code = 201, message = "멤버 생성됨")
  public ResponseEntity<Member> addMember(@RequestBody AddMemberDto dto) {
    return new ResponseEntity<>(
      memberService.addMember(dto),
      HttpStatus.CREATED);
  }

  @Tag(name = "Member")
  @ApiOperation(value = "전체 멤버 조회",
    notes = "DB에 저장된 모든 멤버를 조회합니다. \n가장 최근에 만들어진 멤버가 먼저 나타납니다.")
  @GetMapping("/all")
  @ApiResponse(code = 200, message = "전체 멤버 조회 성공")
  public Iterable<Member> getAllMembers() {
    return memberService.getAllMembers();
  }

  @Tag(name = "Member")
  @ApiOperation(value = "멤버 조회", notes = "요청된 id에 해당하는 멤버를 조회합니다.")
  @GetMapping("/{id}")
  @ApiResponse(code = 200, message = "멤버 조회 성공")
  public Member getMember(@PathVariable Integer id) {
    return memberService.getMember(id);
  }

  @Tag(name = "Member")
  @ApiOperation(value = "멤버 수정", notes = "요청된 id에 해당하는 멤버의 내용을 수정합니다.")
  @PutMapping(path = "/{id}", produces = "application/json")
  @ApiResponse(code = 200, message = "멤버 수정 성공")
  public Member setMember(@PathVariable Integer id,
    @RequestBody SetMemberDto dto) {
    return memberService.setMember(id, dto);
  }

  @Tag(name = "Member")
  @ApiOperation(value = "멤버 삭제", notes = "요청된 id에 해당하는 멤버를 삭제합니다.")
  @DeleteMapping("/{id}")
  @ApiResponse(code = 200, message = "멤버 삭제 성공")
  public void deleteMember(@PathVariable Integer id) {
    memberService.deleteMember(id);
  }
}
</code>
</pre>

# @Tag
swaager에 Tag로 정보를 남길 수 있는 기능

# @RestController
전통적인 Spring MVC의 컨트롤러인 @Controller와 Restful 웹서비으싀 컨트롤러인 @RestController의 주요한 차이점은 HTTP Response Body가 생성되는 방식이다.

@RestController는 @Controller에 @ResponseBody가 추가된 것이다. 당연하게도 RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것이다. 최근에 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 객체를 ResponseEntity로 감싸서 반환한다.

# @RequestMapping
우리는 특정 url로 요청을 보내면 Controller에서 어떠한 방식으로 처리할지 정의를 한다.

이떄 들어온 요청을 특정 메서드와 매핑하기 위해 사용하는 것이 @RequestMapping이다.

@RequestMapping에서 가장 많이 사용하는 부분은 value와 method이다.

value는 요청받을 url을 설정하게 된다. method는 어떤 요청으로 받을지 정의하게 된다.(GET,POST,PUT,DELETE)

# @ApiOeration
요청 URL에 매핑된 API에 대한 설명
# @PostMapping
값 수정할 떄 사용
# @ApiResponse
응답에 대한 설명
# @RequestBody

# @PathVariable
  
