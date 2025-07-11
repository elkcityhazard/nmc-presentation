
---
title: Exploring ArcXP Data Structures
weight: 7
outputs: ["Reveal"]
transition_type: "concave"
---
{{% section %}}
## Part 2: Exploring The Unknown
{{% /section %}}
{{% section %}}
### ArcXP Data Migration Challenges
- Lack of documentation
- Customer Enablement Team was used up quickly and elected to not retain
- Lack of resources on line
- Migrating from headless experience to "block themes"
- Inconsistent apis and data shapes
- Migration API only had unformatted examples of "minimal viable examples"
- Migration API errors were not verbose
{{% /section %}}

{{% section %}}
### What I Did
- First thing I did was used the CMS
    - Created articles with the "default" theme
    - Created assets such as videos, galleries,
      playlists,authors,tags,"sites"
    - Utilized Browser Developer Tools and Burp Suite Proxy to read
      response payloads
    - saved many sandbox articles and assets json payloads into json files
      for reference
{{% /section %}}

{{% section %}}
### Migration API
- A suite of API Endpoints that accept PUT, POST, DELETE Methods and JSON
  endpoints that consist of JSON ANS
- [ARC Native Specification](https://github.com/washingtonpost/ans-schema/tree/master/src/main/resources/schema/ans/0.10.9 "Arc Native Specification")
- __Goal__: Rebuild Content in a format that satisfies ANS
{{% /section %}}

{{% section %}}
### What I Did To Learn Migration API
- Hand Built Small ANS Payloads and used CURL/Postman To familiarize myself
  with the API
- Reached out To Cincinnati News and Click On Detroit who were current
  customers of ArcXP, met with developers to learn from their experience
- Continued to build test case objects to practice with in a sandbox
  environment. 
  {{% /section %}}
  {{% section %}}  
- Detailed when failures would occur, status codes, status messages,
  commonalities of data structures and relationships
- Familiarized Myself with the order / precedence in which data needs to be
  ingested for proper referencing (migration center breaks up payload to
  different ingestion services)
- Familiarized myself with adding any custom data keys
{{% /section %}}

{{% section %}}
### Handling Video
- Migration Center had strict guidelines for video ingestion
    - H.264/30 fps
    - No more than 2GB
- What I Did
    - Created db to house video meta data
    - Called `field 59` API and build a database on filesizes and encoding
    - Built a cli that calls FFMPEG to convert video and update
      a db table with corrected format - file_name, id, article_id,
      field59_id  
{{% /section %}}

{{% section %}}
### Handling Images
- Migration API would only accept: `JPEG`, `PNG`, `BMP`,`TIFF`
- Problem: existing website used many image formats such as `TIFF`, `SVG`,
  `WEBP`
- Solution: similar to above, accept using imagemagick to convert the
  image, store the changes in a db, and handle that in migration
{{% /section %}}

{{% section %}}
### Sites API
- Website sections
- Alternative site sections
- Section metadata
- Social
- Custom Meta keys
- Global Content items such as lead art, logos, etc
{{% /section %}}


{{% section %}}

### Hierarchical API
- Site Navigation
- Section Aliases
{{% /section %}}

{{% section %}}
### Delivery API
- Handling Redirects
- Canonical URLs
- Vanity Urls
{{% /section %}}

{{% section %}}
### Order Matters
- Authors
- Tags
- Categories
- Images
- Galleries
- Videos
- Stories
- "Sites" (also known as sections)

{{% /section %}}
{{% section %}}
### Building A Test Site
- Building a test site to consume content
- Content Sources
    - ArcXP Data
    - Vendor Data
    - Self-hosted Data
{{% /section %}}

{{% section %}}
### Example Of Content Source
```
import axios from "axios";
import { parseString } from 'xml2js';

const fetch = () => {
  // get time rounded down to the last 5 minute interval for cache busting
  const coeff = 1000 * 60 * 5;
  const date = new Date();  //or use any other date
  const rounded = new Date(Math.round(date.getTime() / coeff) * coeff);
  const timeParam = String(rounded.getHours()).padStart(2,'0')+String(rounded.getMinutes()).padStart(2,'0');
  return axios.get(`https://spicymagic.9and10news.com/bti-closings/closings.xml?time=${timeParam}`)
    .then((response)=>{
      let parsedJson;
      // Check for closed Root tag before parsing
      const rootRegex = /<\/File>/ig;
      const rootCheck = response.data.match(rootRegex);
      if(!rootCheck){
        // fix broken root
        response.data+='</File>';
      }

      parseString(response.data, {trim: true, normalizeTags: true, normalize: true, explicitArray: false}, (err, result) => {
        parsedJson = result;
      });

      // move lastUpdated to root
      let lastUpdated = parsedJson.file.$.Time;
      delete parsedJson.file.$;
      parsedJson.file.lastUpdated = lastUpdated;

      // check if closing is singular move to array
      if(parsedJson.file.closing && ! Array.isArray(parsedJson.file.closing)){
        const singleClosing = parsedJson.file.closing;
        delete parsedJson.file.closing;
        parsedJson.file.closing = [singleClosing];
      }

      return parsedJson.file;
    })
    .catch(function (error) {
      const cause = new Error(error.message);
      const errorMsg = new Error('School Closings Get Error', {cause});
      errorMsg.statusCode = 404;
      errorMsg.cause = {
        message:error.message,
        status: error.status
      };
			throw errorMsg;
    });
};

export default {
  fetch,
  schemaName: "910-weather",
  ttl: 300,
  cache: true,
  serveStaleCache: true
};
```
{{% /section %}}

{{% section %}}
### A Minimal Viable ANS Document

```
class BulkANSObj {
    constructor(
                sourceId = new Date(Date.now()).toString(),
                sourceType = "story",
                priority = "historical",
                website = "910news",
                groupId ="",
                ANS = {},
                circulations = [],
                references = [],
                arcAdditionalProperties = {}
    ) {
        this.sourceId = sourceId
        this.sourceType = sourceType
        this.priority = priority
        this.website = website
        this.groupId = groupId
        this.ANS = ANS
        this.circulations = circulations
        this.references = references
        this.arcAdditionalProperties = arcAdditionalProperties

    }
}



module.exports = BulkANSObj

```
{{% /section %}}

