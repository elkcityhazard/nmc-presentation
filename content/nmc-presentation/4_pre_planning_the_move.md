
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
### Choosing A Tech Stack (and why we chose the wrong one)
- 2 frontend and myself as migration
- Tech lead advocated for Node.js due to commonality of working with
  Javascript amongst all three of us
- One developer dropped out
- The lead developer was less familiar with backend development
- Other languages such as (Go, python) would have been better suited for
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
    - wordpress slug (to get data from api)
    - version (in case we had any race condition issues)

{{% /section %}}

{{% section %}}
### Meeting With Departments
- Meeting with department leads and key personnel
- Conducted interviews
    - Important Sections
    - General Workflow
    - Key pages
    - Identified sponsorships
    - Determing pain points and opportunities
{{% /section %}}

{{% section %}}
### Choosing Some Additional Vendors
- Freestar for programmatic ads
- chartbeat for real time analytics in combination with Google Analytics
  (trending and latest stories feed)
- Connatix & Minute.ly for VOD ads
- Mailchimp and wufoo for newsletters and contact forms
- dappier.ai for RAG marketplace revenue share
{{% /section %}}
