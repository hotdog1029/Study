<pre>
<code>
@Entity
@Getter
@Setter
@Builder
@AllArgsConstructor
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Member extends CommonEntity {

  @Id
  @GeneratedValue(
    strategy = GenerationType.SEQUENCE,
    generator = "member_seq")
  private Integer id;

  @NotNull
  private String name;
  @NotNull
  private String email;
}
</code>
</pre>

# @Builder
* 다수의 필드를 가지는 복잡한 클래스의 경우, 생성자 대신에 빌더를 사용하는 경우가 많다. 빌더 패턴을 직접 작성해보면 코딩량이 의외로 상당함을 깨닫게 된다. 이 때, @Builder 어노테이션을 사용하면 자동으로 해당 클래스에 빌더를 추가해주기 때문에 매우 편리하다.

# @AllArgsConstructor
* 모든 필드값을 파라미터로 받는 생성자로 만들어준다.

# @NoArgsConstructor
* 파라미터가 없는 기본 생성자를 생성해준다.

# @RequiredArgsConstructor
* final이나 @NonNUll인 필드 값만 파라미터로 받는 생성자를 만들어준다.

# @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "member_seq")
* JPA가 제공하는 데이터베이스 기본 키 생성 전략은 다음과 같다
* 직접할당: 기본 키를 어플리케이션에서 직접 할당 해주는 방법 (application에서 생성)
* 자동할당: 데이터베이스가 자동으로 할당해주는 방법 (db가 생성)
* 직접할당의 경우, @Id만 사용하면 된다. 자동 생성의 경우, 여러 가지 설정들이 있다. 데이터 베이스 방안들에 따라서 사용할  종류가 나누어짐
* IDENTITY: 기본 키 생성을 데이터베이스에 위임한다. MySQL에서 많이사용, em.persist()를 호출하여 객체를 영속성 상태로 만드는 순간 INSERT SQL이 호출됨, 따라서, 이 전략은 쓰기 지연이 동작하지 않음
* SEQUENECE: 데이터베이스 시퀀스는 유일한 값을 순서대로 생성하는 특별한 데이터베이스 오브젝트이다. SEQUENCE 전략은 이 시퀀스를 사용해서 기본 키를 생성한다. 이 전략은 시퀀스를 지원하는 오라클, PostgreSQL, DB2, H2 데이터베이스에 사용된다.
* SEQUENCE 전챡의 경우, IDENTITY 전략과 코드는 동일하지만, 내부 동작이 다르다. em.persist()를 호출 시, 데이터베이스 시퀀스를 사용해서 식별자를 조회한다. 식별자를 엔티티에 할당한 후에 엔티티를 영속성 컨텍스트에 저장한다. 이후 트랜잭션을 커밋해서 플러시가 일어났을 경우, 엔티티를 데이터베이스에 저장합니다. IDENTITY와의 차이점은 IDENTITY의 경우, 영속성 컨텍스트에 저장하기 위해서 INSERT를 바로 날린다는 점이다.
