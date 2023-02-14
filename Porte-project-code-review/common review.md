# CommonEntity
<pre><code>
@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class CommonEntity extends CommonTimeEntity {

  @CreatedBy
  @Column(updatable = false)
  private String createdBy;

  @LastModifiedBy
  private String lastModifiedBy;
}
</code></pre>


<pre><code>
@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class CommonTimeEntity {

  @CreatedDate
  @Column(updatable = false)
  private LocalDateTime createdDate;

  @LastModifiedDate
  private LocalDateTime lastModifiedDate;
}
}
</code></pre>


@MappedSuperclass

@MappedSuperclass는 상속관계 매핑과는 관련이 없다. 예를 들어 모든 클래스는 생성 시간(createdDate)라는 속성을 가져야 한다고 가정하겠다. 모든 클래스마다 직접 createdDate라는 필드를 붙여줄 수 있지만, createdDate라는 필드를 가진 추상 클래스를 만들어 이를 다른 클래스들이 상속받도록 하는 것이 좀 더 효과적임

즉 이는 공통된 필드를 사용하기 위한 상속을 받은 것이지, 부모와 자식의 관계 혹은 is-a 관계 때문에 상속을 받는 것이 아니다.

createdBy => 누가 생성했는지

createdDate => 언제 생성되었는지

lastModifiedBy => 누가 마지막으로 수정하였는지

lastModifiedDate => 언제 마지막으로 수정하였는지

@EntityListeners

@EntityListeners은 JPA Entity에서 이벤트가 발생할 때마다 특정 로직을 수행할 수 있는 어노테이션임


# 공통적으로 엔티티들이 가져야 하는 생성자,수정자,생성일,수정일을 자동으로 시간을 매핑하여 데이터베이스 테이블에 넣어주는 Audit 기능을 이용한 것
