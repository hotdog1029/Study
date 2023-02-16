<pre>
<code>
@Service
@RequiredArgsConstructor
public class MemberServiceImpl implements MemberService {
  private final MemberRepository memberRepository;

  @Override
  public Member addMember(AddMemberDto dto) {
    Member member = Member.builder()
      .name(dto.getName())
      .email(dto.getEmail())
      .build();

    return memberRepository.save(member);
  }

  @Override
  public List<Member> getAllMembers() {
    return memberRepository.findAllByOrderByIdDesc();
  }

  @Override
  public Member getMember(Integer id) {
    return memberRepository.findById(id).orElseThrow();
  }

  @Override
  public Member setMember(Integer id, SetMemberDto dto) {
    Member member = memberRepository.findById(id).orElseThrow();
    member.setName(dto.getName());
    member.setEmail(dto.getEmail());

    return memberRepository.save(member);
  }

  @Override
  public void deleteMember(Integer id) {
    memberRepository.deleteById(id);
  }

}
</pre>
</code>

# 그냥 기본적인 Repository를 이용한 멤버 생성, 모든 멤버조회, id를통한 멤버조회, 멤버정보변경, 멤버삭제 로직밖에 없음
