# SwaggerConfig

# @EnableWebMvc
스프링 MVC에서 모든 요청의 흐름을 관리하는건 DispatcherServlet이다.

DispatcherServlet은 전달받은 설정 파일을 이용해서 스프링 컨테이너를 생성한다.

DispatcherServlet이 스프링 컨테이너를 생성하기 위해선 입력으로 받는 설정 클래스에는 HanderMapping 빈과 HandlerAdapter 빈이 등록되어있어야 한다. 하지만 설정 클래스에 @EnableWebMvc 어노테이션을 추가해주면 해당 빈을 자동으로 추가해준다.


# @Import(BeanValidatorPluginsConfiguration.class)
Spring Rest API 자동화하는데 추가해줘야하는 어노테이션으로 알고 있자
