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

# @AllArgsConstructor

# @@NoArgsConstructor

# @@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "member_seq")

# @NotNull
