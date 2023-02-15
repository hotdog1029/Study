# AddMemeberDto
<pre>
<code>
@Data
@AllArgsConstructor
@NoArgsConstructor
@ApiModel(value = "멤버 생성", description = "멤버 생성을 위한 dto")
public class AddMemberDto {
  @ApiModelProperty(position = 1, value = "이름", required = true)
  private String name;
  @ApiModelProperty(position = 2, value = "이메일")
  private String email;
}
</code>
</pre>

# SetMemeberDto
<pre>
<code>
@Data
@AllArgsConstructor
@NoArgsConstructor
@ApiModel(value = "멤버 수정", description = "멤버 수정을 위한 dto")
public class SetMemberDto {
  @ApiModelProperty(position = 1, value = "이름", required = true)
  private String name;
  @ApiModelProperty(position = 2, value = "이메일")
  private String email;
}
</code>
</pre>

DTO를 말 그대로 해석하면 "데이터 전송 객체"가 된다. 즉, 데이터의 전송을 담당하는 클래스라는 소리이다.
