# Lombok이란?
Lombok 프로젝트는 자바 라이브러리로 코드 에디터나 빌드 툴(인텔리제이, 이클립스 등)에 추가하여 코드를 효율적으로 작성할 수 있도록 도와준다. class명 위에 어노테이션을 명시해줌으로써 getter나 setter, equals와 같은 method를 따로 작성해야 하는 번거로움을 덜어준다.

# @Data
@Data 어노테이션은 @Getter / @Setter / @ToString / @EqualsAndHashCode와 @RequireArgsConstructor 를 합쳐놓은 종합 선물 세트라고 할 수 있다.

그냥 롬북의 유용한 어노테이션을 한꺼번에 호출을 하는 것

Data 어노테이션은 callSuper, includeFieldName, exclude와 같은 파라미터와 같이 사용될 수 없으므로, 해당 파라미터 사용이 필요할 때는 개별 어노테이션을 따로 다 명시해주면 된다.
