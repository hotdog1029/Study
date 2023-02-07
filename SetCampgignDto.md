# SetCampgignDto 코드리뷰

<pre>
<code>
@Data
@AllArgsConstructor
@NoArgsConstructor
@ApiModel
public class AddCampaignDto {
  @ApiModelProperty(position = 1, value = "캠페인명", required = true)
  private String name;
  @ApiModelProperty(position = 2, value = "목표")
  private String purpose;
  @ApiModelProperty(position = 3, value = "실행기간")
  private String duration;
  @ApiModelProperty(position = 4, value = "예산", example = "0")
  private Long budget;
  @ApiModelProperty(position = 5, value = "상품", required = true, example = "0")
  private Integer product;
}
</code>
</pre>

## @Data
