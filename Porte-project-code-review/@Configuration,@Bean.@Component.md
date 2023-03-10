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
</pre>


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
</pre>

@Configuration 안에서 @Bean이 빈으로 등록되는 과정은 간단하다. 스프링 컨테이너는 @Configuration이 붙어있는 클래스를 자동으로 빈으로 등록해두고, 해당 클래스를 파싱해서 @Bean이 있는 메소드를 찾아서 빈을 생성해준다. 하지만 어떤 임의의 클래스를 만들어서 @Bean 어노테이션을 붙인다고 되는 것이 아니고, @Bean을 사용하는 클래스에는 **반드시 @Configuration 어노테이션을 활용하여** 해당 클래스에서 Bean을 등록하고자 함을 명시해주어야 한다. 스프링 빈으로 등록된 다른 클래스 안에서 @Bean으로 직접 빈을 등록해주는 것도 동작은 한다. 하지만 @Configuration안에서 @Bean을 사용해야 싱글톤을 보장받을 수 있으므로 @Bean 어노테이션은 반드시 @Configuration과 함께 사용해주어야 한다.

이러한 @Bean 어노테이션의 경우는 수동으로 빈을 직접 등록해줘야만 하는 상황인데, 주로 다음과 같을 때 사용한다.

1. 개발자가 직접 제어가 불가능한 라이브러리를 활용할 때
2. 애플리케이션 전범위적으로 사용되는 클래스를 등록할 때
3. 다형성을 활용하여 여러 구현체를 등록해주어야 할 때

예를 들어 우리가 객체를 Json 메세지로 변경하기 위해 Gson과 같은 외부 라이브러리를 사용한다고 하자. 그러면 해당 클래스를 싱글톤 빈을 등록해주어야 1개의 객체만 생성하여 여러 클래스가 공유함으로써 메모리 상의 이점을 얻을 수 있을 것이다. 그런데 해당 클래스는 우리가 만든게 아니라 가져다 쓰는 클래스일 뿐 불가피하게 @Bean으로 등록해줘야만 한다.

애플리케이션 전범위적으로 사용되는 클래스와 다형성을 활용하여 여러 구현체를 등록할 떄 @Bean을 사용하면 좋은 이뉴는 한 눈에 파악하여 유지보수하기 좋기 때문이다. 예를 들어 여러 구현체를 빈으로 등록해줄 때 어떠한 구현체들이 빈으로 등록되는지를 파악하려면 소스 코드를 찾아볼 필요 없이 해당 @Configuration 클래스만 보면 되기 때문이다.

# @Component
하지만 이렇게 수동으로 직접 빈을 등록하는 작업은 빈으로 등록하는 클래스가 많아질수록 상당히 많은 시간을 차지할 것이고, 생산력 저하를 야기할 것이다. 그래서 스프링에서는 특정 어노테이션이 있는 클래스를 찾아서 빈으로 등록해주는 컴포넌트 스캔 기능을 제공한다.

스프링은 컴포넌트 스캔을 사용해 @Component 어노테이션이 있는 클래스들을 찾아서 자동으로 빈 등록을 해준다. 그래서 우리가 직접 개발한 클래스를 빈으로 편리하게 등록하고 하는 경우에는 @Component 어노테이션을 활용하면 된다.

@Component를 갖는 어노테이션으로 @Controller, @Service, @Repository 등이 있으며 앞서 살펴봤던 @Configuration 역시 안에 @Component를 가지고 있다.
