# Swagger
Swagger는 anntation 기반의 REST API 문서를 만들어주는 프레임워크이다.

다음과 같이 간단하게 dependency를 추가하여 사용할 수 있다.

<pre>
<code>
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-swagger2</artifactId>
  <version>2.9.2</version>
</dependency>
</code>
</pre>

# Annotaion 종류
@Api:Swagger 리소스로 사용될 클래스를 마킹

@ApiImplicitParam:	Api 의 파라미터(하나)

@ApiImplicitPrams:	Api 의 파라미터(value ={} 로 @ApiImplicitParam 을 여러개 포함할 수 있음)

@ApiModel: Swagger model 에 정보를 추가(모델 클래스)

@ApiModelProperty	model 의 프로퍼티 정보

@ApiOperation	http method 에 대한 api 정보

@ApiParam	api 파라미터에 직접 설명을 붙임

@ApiResponse	api 응답에 관한 정의

@ApiResponses	api 응답에 관한 정의(value ={} 로 @ApiResponse 을 여러개 포함할 수 있음)

@Authorization	권한에 대한 설명

@AuthorizationScope	oauth2 의 authorization scope에 대해 설명
