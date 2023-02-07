# 1) DAO
DAO(Data Access Object)는 데이터베이스의 data에 접근하기 위한 객체이다. 

실제로 DB에 접근하여 data를 삽입, 삭제, 조회, 수정 등 CRUD 기능을 수행한다.

Service와 DB를 연결하는 고리 역할을 한다.

Repository pakage가 바로 DAO이다.

# 2) DTO(Data Transfer Object)
DTO는 계층간 (Controller, view, Business Layer) 데이터 교환을 위한 자바 빈즈(Beans)를 의미한다.

DTO는 로직을 가지지 않는 데이터 객체이고 getter/setter 메소드만 가진 클래스를 의미한다.

DB에서 데이터를 얻어서 Service나 Controller 등으로 보낼 때 사용한다.

즉 엔티티를 DTO 형태로 변환한 후 사용한다.

# 3) VO(value Object)
VO는 DTO와 달리 Read-Only속성을 지닌 값 오브젝트이다. DTO는 setter를 가지고 있어서 값이 변할 수 있지만 VO의 경우에는 getter만 가지고 있어서 수정이 불가능하다.

DTO와 VO의 차이점은 DTO는 인스턴스 개념이고, VO는 리터럴 값 개념이다.

VO는 값들에 대해 Read-Only를 보장해줘야 존재의 신뢰성이 확보되지만 DTO의 경우에는 단지 데이터를 담는 그릇의 역할일 뿐 값은 그저 전달되어야 할 대상일 뿐이다.

# 4) Entity
Entity 클래스는 실제 DataBase의 테이블과 1 : 1로 매핑되는 클래스로, DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로 가져야 한다.

Entity 클래스는 상속을 받거나 구현체여서는 안되며, 테이블내에 존재하지 않는 컬럼을 가지면 안된다.

## 4.1 Entity, DTO Class 분리 이유
Entity와 DTO를 분리해서 관리해야 하는 이유는 DB Layer와 View Layer 사이의 역할을 분리하기 위해서이다.

Entity 클래스는 실제 테이블과 매핑되어 만일 변경되게 되면 여러 다른 클래스에 영향을 끼치고, DTO 클래스는 VIew와 통신하며 자주 변경되므로 분리 해주어야 한다.

## 4.2 Entity Setter 금지 및 생성자, 접근 제어
Entity를 작성할 때, setter를 무분별하게 사용하면 객체(Entity)의 값을 변경할 수 있으므로 객체의 일관성을 보장할 수 없다.

객체의 일관성을 유지할 수 있어야 유지 보수성이 올라가기 때문에 setter를 사용해서는 안되며, 객체의 생성자에 값들을 넣어줌으로써 setter 사용을 줄일 수 있다.
