# CampaignRepository 코드 리뷰

<pre>
<code>
package com.tmax.mt.campaign;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;

public interface CampaignRepository extends JpaRepository<Campaign, Integer> {
  public List<Campaign> findAllByOrderByIdDesc();
}
</code>
</pre>

# JpaRepository란?
JPA는 인터페이스로 객체를 리포지토리에 기본적으로 CRUD하는 인터페이스를 제공한다.

findById, findAll, save 등

즉, 대부분의 엔티티에서 반복적으로 사용되는 단순 쿼리들을 Spring Data JPA가 인터페이스 형태의 메소드로 만들어 놓고 Hibernate가 애플리케이션이 실행될 때 엔티티에 맞춰서 동적으로 구현해서 우리는 필요할 때 메소드만을 불러서 사용할 수 있게 해주는 것이다.

