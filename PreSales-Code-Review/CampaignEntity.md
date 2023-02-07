<pre>
<code>
@Entity
@Getter
@Setter
@Builder
@AllArgsConstructor
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Campaign extends CommonEntity {

  @Id
  @GeneratedValue(strategy = GenerationType.SEQUENCE,
    generator = "campaign_seq")
  private Integer id;

  @NotNull
  private String name;
  private String purpose;
  private String duration;

  @NotNull
  private String state;

  private Long budget;
  @NotNull
  private Long cost;

  @NotNull
  private Integer product;

  private Integer target;
  private Integer content;
  private Integer channel;
  private Integer performance;
}
</code>
</pre>

