# CampaignServicelmpl 코드 리뷰

# 1)
<pre>
<code>
  @Override
  public Campaign addCampaign(AddCampaignDto dto) {

    Campaign campaign = Campaign.builder()
      .name(dto.getName())
      .purpose(dto.getPurpose())
      .duration(dto.getDuration())
      .state("저장됨")
      .budget(dto.getBudget())
      .cost(0L)
      .product(dto.getProduct())
      .target(null)
      .content(null)
      .channel(null)
      .performance(null)
      .build();
    return campaignRepository.save(campaign);
  }
</code>
</pre>

Builder를 이용해서 캠페인을 추가한 후 캠페인리포지토리에 저장후 반환

# 2)

<pre>
<code>
  @Override
  public Iterable<Campaign> getAllCampaigns() {
    return campaignRepository.findAllByOrderByIdDesc();
  }

  @Override
  public Campaign getCampaign(Integer id) {
    return campaignRepository.findById(id).orElse(null);
  }

  @Override
  public Campaign setCampaign(Integer id, SetCampaignDto dto) {

    Campaign campaign = campaignRepository.findById(id).orElseThrow();
    campaign.setName(dto.getName());
    campaign.setPurpose(dto.getPurpose());
    campaign.setDuration(dto.getDuration());
    campaign.setBudget(dto.getBudget());
    campaign.setProduct(dto.getProduct());
    campaign.setTarget(dto.getTarget());
    campaign.setContent(dto.getContent());
    campaign.setChannel(dto.getChannel());

    return campaignRepository.save(campaign);
  }

  @Override
  public void deleteCampaign(Integer id) {
    campaignRepository.deleteById(id);
  }
</code>
</pre>

순서대로 campaignRepository.findAllByOrderByIdDesc()을 이용하여 모든 캠페인 조회

campaignRepository.findById(id).orElse(null)을 이용하여 id를 이용하여 캠페인을 찾고 찾는 캠페인이 없다면 null값 반환

SetCampaign은 id를 통해서 캠페인을 찾고 해당 캠페인의 인자값을 새로 셋팅함 그리고 .save를 이용하여 저장후 반환

마지막은 id를 이용하여 캠페인을 찾아 삭제하는 기능
