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
그냥 롬북의 유용한 어노테이션(@Getter, @Setter, @ToString, @RequireArgsConstructoer 등)을 한꺼번에 호출을 하는 것

## @~Constructoer

@NoArgsConstructor => 파라미터가 없는 기본 생성자를 생성

@AllArgsConstructor => 모든 필드 값을 파라미터로 받는 생성자를 만듦

@RequiredArgsConstructor => final이나 @NonNull인 필드 값만 파라미터로 받는 생성자 만듦

## @ApiModel
@ApiModel: Swagger model 에 정보를 추가(모델 클래스)

## @ApiModelProperty
@ApiModelProperty를 사용하는 DTO Class Field에 추가하면, 해당 DTO Field의 에제 Data를 추가할 수 있다.


