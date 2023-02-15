# DTO(Data Transfer Object)
DTO를 말 그대로 해석하면 **"데이터 전송 객체"** 가 된다. 즉, 데이터의 전송을 담당하는 클래스이다.

물론 DTO 클래스가 웹 서비스에 국한되어 사용하는 클래스는 아니지만 현재 공부하고 있는 SpringBoot framwork가 주로 웹 서비스 백엔드 구축에 많이 쓰이니 그를 기준으로 정리해보겠다.

DTO는 웹 서비스의 클라이언트와 서버, 더 자세히는 클라이언트와 서버 서비스 계층 사이에서 교환되는 데이터를 담는 그릇이다.

서버에 다음과 같은 간단한 엔티티가 있다고 가정하자.
<pre>
<code>
@Getter
@Setter
@Entity
public class Post() {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    Long id;
    
    String title;
    
    String content;
    
    String author;
}
</code>
</pre>

클라이언트는 위 엔티티의 데이터를 저장하기 위해 title, content, author에 대한 정보를 담아 서버에 Request를 보낼 것이다.

이 떄, 서버에서 가장 먼저 일어나야 하는 일은 무엇일까

그렇다. 데이터를 받아야 한다! (사실 따지고 보면 가장 먼저는 아니지만 직관적으로 봤을 때) 이 때 등장하는 것이 DTO 클래스이다.

<pre>
<code>
@Getter
@NoArgsConstructor
public class PostSaveRequestDto {
    private String title;
    private String content;
    private String author;
}
</code>
</pre>

DTO 클래스는 클라이언트의 Request_body에 있는 Entity의 필드들을 담아 다음 로직(저장, 수정 등)을 처리하는 곳으로 데이터를 넘겨준다. 물론 반대로 서버 쪽에서 클라이언트 쪽으로 응답(Reponse)을 보낼 때도 이런 DTO 클래스를 이용하면 된다.

Django 개발을 하셨던 분이라면 Django Rest framework의 Serializer 클래스를 생각하면 된다.

그런데 Post 클래스와 PostsaveRequestDto의 필드가 같은데 그럼 데이터를 Post class로 바로 받으면 되지 않을까? 라는 생각이 들 수도 있다.

이것은 틀린 생각이다. Entity 클래스는 데이터베이스와 맞닿은 핵심 클래스이다. 클라이언트 쪽의 변경은 빈번히 일어날 수 있는데 그에 따라 데이터 베이스의 스키마가 변경되는 것은 매우 큰 비용이기 때문이다.

사실 따져볼 것도 없이 기본적으로 Post 클래스가 Entity 클래스의 역할도 하고 데이터를 받는 일도 한다면 객체 지향의 기본 원칙인 SOLID원칙 중 SRP(Sigle Responsibility Principle)을 위배한 것이 되니 당연히도 분리해야 하는 것이 맞다.


