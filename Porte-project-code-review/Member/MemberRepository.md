<pre>
<code>
public interface MemberRepository extends JpaRepository<Member, Integer> {
  public List<Member> findAllByOrderByIdDesc();
}
</code>
</pre>

# JpaRepository
* JPARepositoy는 인터페이스이다. JPARepositoy는 미리 검색 메소드를 정의 해 두는 것으로, 메소드를 호출하는 것만으로 스마트한 데이터 검색을 할 수 있게 되는 것이다.
* JPQL과 같은 쿼리문을 짤필요가 없음
* Entity에 있는 데이터를 조회하거나 저장과 변경 그리고 삭제를 할때 Spring JPA에서 제공하는 Repository라는 인터페이스를 정희해 해당 엔티티의 데이터를 사용할 수 있음
