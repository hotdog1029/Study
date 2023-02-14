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
