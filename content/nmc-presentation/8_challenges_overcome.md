
---
title: Challenges Overcome
weight: 9
outputs: ["Reveal"]
transition_type: "concave"
---

{{% section %}}
### Challenges Overcomes
Some challenges we encountered migrating data
{{% /section %}}

{{% section %}}
### Lack Of Concurrency
- Many issues would have been solved via concurrency
- challenges ocurred from bottlenecks in network io
- Order of content ingestion mattered, passing to a routine handler would
  have helped via for select pattern
{{% /section %}}

{{% section %}}
### Memory Management
- I ran into many cases where asset processing routinely exhausted heap
- Solution in these cases was to convert many file io operations (temp
  files,etc) to use buffers and manage io streams which helped  
{{% /section %}}

{{% section %}}
### Rate Limiting
- This was by far the biggest pain
- Tried many header manipulation hacks
- Ended up on a combination of burpsuite and mullvad vpn cli as part of
  shell script to rotate ip
{{% /section %}}

{{% section %}}
### Media Types / File Sizes
- Had to build separate subprograms to convert media
- Store in separate database to act as a reference update
- This added to memory overhead
{{% /section %}}

{{% section %}}
### Inconsistent Data Format / Unclean
- This was the primary motivation for developing V2 CLI Tool
- Data was so inconsistent through epochs that it required many sub
  programs to process data into ANS
{{% /section %}}

{{% section %}}
### Scope creep
- Leadership identified many items that weren't of value from a data
  standpoint but were of sentimental value
- Consistent prioitization and communication helped solve many of these
  issues
{{% /section %}}

{{% section %}}
### Staff Resource Limitation
- Developer left early in project requiring to rebalance
- Gave less time to migration as I needed to jump into development
{{% /section %}}

{{% section %}}
### Storing UGC Data
- Arc custom fields are very limited and don't work across all APIs
- User generated content from the previous site needed to be hosted in it's
  own microservice
{{% /section %}}

{{% section %}}
### Vendor and 3P Data Integrations
- Lots of integrations written haphazardly in WP Theme and drop in plugins
- Resources needed to be allocated to build content sources and any API
  services
{{% /section %}}
