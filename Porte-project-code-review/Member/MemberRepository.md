<pre>
<code>
public interface MemberRepository extends JpaRepository<Member, Integer> {
  public List<Member> findAllByOrderByIdDesc();
}
</code>
<pre>

# JpaRepository
* JPARepositoy는 인터페이스이다. JPARepositoy는 미리 검색 메소드를 정의 해 두는 것으로, 메소드를 호출하는 것만으로 스마트한 데이터 검색을 할 수 있게 되는 것이다.
* JPQL과 같은 쿼리문을 짤필요가 없음
* 
