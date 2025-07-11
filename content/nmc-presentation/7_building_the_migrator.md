---
title: Building The Migrator
weight: 8
outputs: ["Reveal"]
transition_type: "concave"
---

{{% section %}}
## Part 3: Building V1 Migration Tool
{{% /section %}}

{{% section %}}
### Strategy
- crawl existing website page by page via wp api
- lookup in db
- parse the document
    - authors
    - images/galleries
    - videos
    - categories/tags
    - html content
    - embedded content
{{% /section %}}

{{% section %}}
### Tools
- crypto package for base32 encoded arcxp ids
- cherrio / jsdom for parsing html
- connect-timeout to handle timeouts and retries
- dotenv to manage environment variables
- node-fetch/promise-request to handle fetching data
- slugify
- xml2js to handle xml to js parsing for json
- yargs for command line args

{{% /section %}}

{{% section %}}
### Prep
- creating up and down migrations
- db servicer
- creating javascript models/interfaces
- creating functions to perform transformations
- additional parser helpers and utilty functions
{{% /section %}}


{{% section %}}
### Mistakes were made
- extremely error prone
- data was extremely messy / difficult to handle edge cases
- lots of failures and logging to log files
- time spent checking is_processed in db 
- memory limitations on local machine
- less discretionary input from myself


{{% /section %}}

{{% section %}}
### Bottlenecks
- restarting often
- rechecking db
- tightly coupled code
{{% /section %}}


{{% section %}}

### Part Migration Tool V2
Creating A CLI with command flags
{{% /section %}}


{{% section %}}
### Why It Was Better
- More control over how the data was processed
- using different sub programs for different eras of the site
- being able to target specific content types on the existing site
  (gallery,photo)
- Although slightly more work, better outcomes due to higher control,
  smaller data sets
- Better memory control
- Easier Testing
{{% /section %}}


{{% section %}}
### How It Worked
- Command line flags
- operate on subset of data
- easier to mock data for testing
- different subroutines for different data structures
- faster i/o operations to track progress, failures, successes
{{% /section %}}
{{% section %}}
     `migrate -DSN="" -section="/news/local" -subprogram="some_subprog" -type="photos" --dry-run=false -verbose=true`

{{% /section %}}
{{% section %}}
- Parse the flags
- switch on each flag
- start sub programs
- process old site into new site
- store results in database
- log errors to error log
- extend and increment as needed
{{% /section %}}
{{% section %}}
### Benefits to CLI
- could write new sub programs as needed
- fine-grained control
- showing stakeholders progress more quickly
- easier mocking for unit and integration tests
- higher degree of portability
- less spaghetti code
- Individual Concerns
{{% /section %}}
 

 ---
### RSS Feed

 - [Our RSS Feed Generator](https://github.com/amledigital/OBF-Starter "910
   Media Group RSS Feed Generator")
 - [Link To A RSS Tool I built](https://github.com/amledigital/weather-map-rss "Weather Map RSS Feed")
 - creating a producer for our web view app
 - mapping arcxp json to rss for consumption to app, google news, apple
   news, etc
 - feeding AI for embeddings






