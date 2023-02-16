<pre>
<code>
@Data
@AllArgsConstructor
@NoArgsConstructor
@ApiModel(value = "프로젝트 수정", description = "프로젝트 수정을 위한 dto")
public class SetProjectDto {
  @ApiModelProperty(position = 1, value = "프로젝트명", required = true)
  private String name;
  @ApiModelProperty(position = 2, value = "프로젝트 설명")
  private String contents;
}
</code>
<pre>

# @Data
* @Data 어노테이션은 @Getter, @Setter, @ToString, @EqualsAndHashCode, @RequireArgsConstructor를 다 모아 놓은 것

# ApiModel
