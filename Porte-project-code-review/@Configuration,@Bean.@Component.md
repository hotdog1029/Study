기존의 Spring MVC에서는 xml을 활용하여 Bean에 등록하고 있었다. 하지만 프로젝트의 규모가 커짐에 따라 사용하는 요소들을 xml에 등록하는 것이 상당히 번거로워 져서 어노테이션을 활용한 Bean 등록 방법이 탄생하게 되었다.

# Spring Bean이란?
Spring에서는 Spring의 DI Container에 의해 관리되는 POJO를 Bean이라고 부르며, 이러한 Bean들은 Spring을 구성하는 핵심 요소이다.

POJO(Plain Old Java Object)로써 Spring 애플리케이션을 구성하는 핵심 객체이다.

Spring IoC 컨테이너 또는 DI 컨테이너에 의해 생성 및 관리된다.

# Spring Bean 등록 방법
예를 들어 다음과 같은 클래스가 있고, 이를 스프링 컨테이너에 등록하고자 한다고 하자.
<pre>
<code>
public class MangKyuResource {

}
</code>
<pre>


이 클래스를 빈으로 등록하기 위해서는 명시적으로 설정 클래스에서 @Bean 어노테이션을 사용해 수동으로 스프링 컨테이너에 빈을 등록하는 방법이 있다. 설정 클래스는 다음과 같이 @Configuration 어노테이션을 클래스에 붙여주면 되는데, @Bean을 사용해 수동으로 빈을 등록해줄 때에는 메소드 이름으로 빈 이름이 결정된다. 그러므로 중복된 빈 이름이 존재하지 않도록 주의해야 한다.

<pre>
<code>
@Configuration
public class ResourceConfig {

    @Bean
    public MangKyuResource mangKyuResource() {
        return new MangKyuResource();
    }

}
</code>
<pre>

@Configuration 안에서 @Bean이 빈으로 등록되는 과정은 간단하다. 스프링 컨테이너는 @Configuration이 붙어있는 클래스를 자동으로 빈으로 등록해두고, 해당 클래스를 파싱해서 @Bean이 있는 메소드를 찾아서 빈을 생성해준다. 하지만 어떤 임의의 클래스를 만들어서 @Bean 어노테이션을 붙인다고 되는 것이 아니고, @Bean을 사용하는 클래스에는 **반드시 @Configuration 어노테이션을 활용하여** 해당 클래스에서 Bean을 등록하고자 함을 명시해주어야 한다. 스프링 빈으로 등록된 다른 클래스 안에서 @Bean으로 직접 빈을 등록해주는 것도 동작은 한다. 하지만 @Configuration안에서 @Bean을 사용해야 싱글톤을 보장받을 수 있으므로 @Bean 어노테이션은 반드시 @Configuration과 함께 사용해주어야 한다.

이러한 @Bean 어노테이션의 경우는 수동으로 빈을 직접 등록해줘야만 하는 상황인데, 주로 다음과 같을 때 사용한다.
1. 
