---
layout: post
title: Work with Toggl API
category: code
tags: api
---

Since I have decided to use Toggl as my time-tracking tool, it is very important for me to get my hand dirty with Toggl API.

<!--more-->

Toggl has a really nice [API](https://github.com/toggl/toggl_api_docs) doc for you to start to manipulate anything without even open the real Toggl App.

#### Authentication

There are two basic ways to authenticate yourself, either by API token, or by username & password. API token could be find in the last line on Toggl Account Setting. I am pretty sure that you have a good knowledge of your own username and password.

Note: Toggl API doc use curl, you could use whatever you choose. For people who have no idea about [curl](https://curl.haxx.se/), it is a command line tool to initiate request to third-party API.

token:
`curl -v -u 1971800d4d82861d8f2c1651fea4d212:api_token -X GET https://www.toggl.com/api/v8/me`

username & password:
`curl -v -u john.doe@gmail.com:secret -X GET https://www.toggl.com/api/v8/me`

#### Start Logging

Let's start logging by creating a time entry.

```
curl -v -u 1971800d4d82861d8f2c1651fea4d212:api_token \
    -H "Content-Type: application/json" \
    -d '{"time_entry":{"description":"driving","pid":28454980,"created_with":"curl"}}' \
    -X POST https://www.toggl.com/api/v8/time_entries/start
```