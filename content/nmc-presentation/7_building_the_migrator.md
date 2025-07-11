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
```
SELECT p.article_id, p.is_processed 
FROM processed AS p WHERE id = ?

```
{{% /section %}}


{{% section %}}

### Migration Tool V2
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
     `migrate -DSN="" -section="/news/local" -subprogram="some_subprog"
-type="photos" --dry-run=false -verbose=true`

{{% /section %}}
{{%section %}}
### Benefits to CLI
- could write new sub programs as needed
- fine-grained control
- showing stakeholders progress more quickly
- easier mocking for unit and integration tests
- higher degree of portability
- less spaghetti code
- Individual Concerns
{{% /section %}}
