
---
title: Determing Existing Data Structures
weight: 6
outputs: ["Reveal"]
transition_type: "concave"
---

{{% section %}}
## Phase 1: Exploring Data
{{% /section %}}

{{% section %}}
### Overview Of TownNews Data
- Articles mostly followed conventional WP Data structures
- Videos all hosted in __Field59__ Cloud Video Service Microservice
- Galleries && Images hosted in proprietary microservice
- Authors are WP Users with some custom meta fields
- A mixture of categories tags with nested taxonomies for site structure
- [TN / Blox/ Field59 API Docs](https://www.help.bloxdigital.com/field59/api/ "Existing Vendor API")
{{% /section %}}

{{% section %}}
### TownNews Challenges
- Contract made us a renter of our data
- Unwilling to give us access to server or plugins to export database
- Unwilling to give us api keys for micro services
- Heavy rate limiting
- WP API was available, but heavily relied on referential relationships
- Typecasting, default values
{{% /section %}}

{{% section %}}
### What I Did
- WP API Endpoints were available and for posts gave a mostly detailed
  representation of the data
-  A combination of BurpSuite and mullvad vpn proxy to bypass rate limit
{{% /section %}}
{{% section %}}
- Utilized wayback machine to find old documentation to learn how to
  reverse engineer their video and gallery api keys
    - combination of hmac signature based on your account id and timestamp
    - pass as part of basic authorization header
{{% /section %}}
{{% section %}}
### Exploring and modeling the data
- Utilized the API documentation and POSTMAN to explore Data Structures
- Created a JSON Schema spec of the data structures of common data
  keys, noting how the relationships map to the WP posts, as well as
  noting anything that wasn't critical to the data (pingback,
  tn metadata)
- Mapping out cat/tags to site sections, storing in database
{{% /section %}}


{{% section %}}
### Legacy Web Data
- Scraped and converted to static html and served from our own server
- Deprecated in 2025
{{% /section %}}

{{% section %}}
### Analyzing Existing External & Vendor Integrations
- 3 Drop In Plugins
- BTI School Closing
- Ski Report API
- Elections Results

{{% /section %}}


