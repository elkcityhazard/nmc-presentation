
---
title: Initial Assessment
weight: 4
outputs: ["Reveal"]
transition_type: "concave"

---
{{% section %}}

# Initial Assessment

From pre-contemplation to contemplation

{{% /section %}}

{{% section %}}
### Weaknesses Of Existing Site
- 18,000 articles & pages
- crawl bloat
- Pagination was taking 5-10 seconds
- Unoptimized search
- Inconsistent data schema resulted in many broken pages, custom pages,
  legacy php or ASP.NET pages requiring higher overhead
- Inconsistent structure tags, pages, posts, categories, random directory
  plugins
  {{% /section %}}

  {{% section %}}
- Video, Photos, Galleries, Podcasts behind vendor gardens with no direct
  access
- Tragedy of the commons
- Shared server space
- Poorly optimized queries and page loading resulting in excess use of
bandwidth
- Lack Of Security Updates
- Lack Of Code Maintenanace
- Poor Dependency Management, Tightly coupled code
- Inconsistent code styles due to many developers
{{% /section %}}

{{% section %}}

### Weaknesses Of ArcXP
- Relatively new product, still in active development, very much a beta
- Lack of documentation
- No plugin ecosystem
- Poor theming environment
- Editors unfamiliar with workflows
- Only a provider, never a consumer
- Absolutely Zero Migration support
- AWS costs
- Inconsistent APIs
- Despite being NOSQL DB, strict schemas

{{% /section %}}

{{% section %}}
 ### Strengths Of ArcXP
 - Owned by WaPo / Amazon with all in one service/cost structure for AWS
    - MediaLive - streaming delivery
    - Elastic Transcoder - m3u8 to hls encoding on the fly
    - Elemental Live - live encoding 
    - Elasticache
    - Lamba serverless functions
- Heavily Focused On Newsrooms
- Integrations With Chartbeat, Elastic Search
- Although unfinished, an impressively large api suite

{{% /section %}}

