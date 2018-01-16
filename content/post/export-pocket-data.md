---
title: "Export Pocket Data"
date: 2018-01-15
tags: ["pocket", "bash", "curl", "linux", "ubuntu"]
draft: false
---

I use [Pocket] mainly to save articles for later reading, and archive them if they are worth a reference at a later time. You can pretty much *Pocket* anything such as links, videos, and images. My bookmarks now only contain sites that I frequent, and financial sites to lessen the chance of link hijacking when searching for the site on Google.

Similar to my last post [Export Pushbullet Pushes], I wanted to export all my Pocket data in text format so I wrote this bash script:

```
#!/bin/bash

# see https://getpocket.com/developer/docs/v3/retrieve

consumerkey=$1
accesstoken=$2

curl \
--header "Content-type: application/json" \
--request POST \
--data "{\"state\": \"all\", \"sort\": \"newest\", \"detailType\": \"complete\", \"consumer_key\": \"$consumerkey\", \"access_token\": \"$accesstoken\"}" \
https://getpocket.com/v3/get > export

jq ".list[] | {sort_id: .sort_id, title: .resolved_title, url: .resolved_url, excerpt: .excerpt}" export > pocket-export.json
```

[Pocket]: https://getpocket.com/
[Export Pushbullet Pushes]: https://www.kevinbarroga.me/post/export-pushbullet-pushes/
