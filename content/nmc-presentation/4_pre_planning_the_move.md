
---
title: Pre-Planning Assessment
weight: 5
outputs: ["Reveal"]
transition_type: "concave"
---

{{% section %}}
## Cleaning and Organizing Data
{{% /section %}}

{{% section %}}
### Choosing A Tech Stack (Why we chose javascript)
- 2 frontend and myself as migration
- Tech lead advocated for Node.js due to commonality of working with
  Javascript amongst all three of us
- The lead developer was less familiar with backend development
  this
{{% /section %}}


{{% section %}}
### Preparation For The Move
- Writing a tool to combine Google Analytics with TownNews Proprietary
  Analytics system
  - Node.js, cheerio, jsdom
  - Google UA API
  - TN Web Scraping via query params
  - Building a CLI to aggregate UA with server analytics of TN
  {{% /section %}}
  {{% section %}}
  - Total of ~ 10,000 posts/pages to migrate
  - Building a mariadb database of pages with at least 100 views a year
    - id
    - slug
    - title
    - wordpress_id
    - version (in case we had any race condition issues)

{{% /section %}}

{{% section %}}
### Meeting With Departments
- Meeting with department leads and key personnel
- Conducted interviews
- Determing pain points and opportunities
{{% /section %}}

