---
title: "Export Pushbullet Pushes"
date: 2018-01-13
tags: ["pushbullet", "bash", "linux", "ubuntu"]
draft: false
---

[Pushbullet] is a pretty cool service that I used for some time to send files and links to my other devices. I also used it to mirror Android notifications on my PCs.

I wanted to export all my pushes in text format so I wrote a small bash script:

```
#!/bin/bash

# see https://docs.pushbullet.com/#list-pushes

apitoken=$1
n=0
cursor=''

while true; do
  curl --header "Access-Token: $apitoken" \
     --data-urlencode active="true" \
     --data-urlencode modified_after="0" \
     $cursor \
     --get \
     https://api.pushbullet.com/v2/pushes > pbexport-${n}

   nextpage=$( jq ".cursor" pbexport-${n} | sed s/\"//g )
   if [ $nextpage == null ]; then
       break
   fi

   jq ".pushes[] " pbexport-${n} >> pushes.json

   sleep 1
   cursor="--data-urlencode cursor=$nextpage"
   n=$[n + 1]
done

```


[Pushbullet]: https://www.pushbullet.com/
