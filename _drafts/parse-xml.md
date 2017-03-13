---
layout: post
title: parse XML
category: code
tags: XML rails
---

For the past two weeks, I am building multiple services to interact with different third-party APIs. From what I experienced, there are general two types of response, `JSON` and `XML`.  

<!--more-->

Note: the difference between two response, the one coming from ESI and the one coming from Barefoot? Why on the earth they will response differently

### Hash.from_xml
-> source code, library(REXML)- lots of restriction resulting from that
### Nokogiri
-> still awful structure...
### Issues
#### >10k string
REXML, security concerns
#### multiple root
no idea why both parser does not work
have to use Nokogiri::HTML parser
#### same key causing problem when converting to hash
be it super nested, or multiple root
### Reflection