---
title: "Creating a New Entry in the Send To Menu"
date: 2025-07-03T21:22:20+05:00
description: ""
url: "/create-a-custom-entry-in-send-to/"
tags:
    - Linux
    - notes-for-self
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: false
---
**For Thunar,** the send to path is located at `~/.local/share/Thunar/sendto/`
* If you want to add a new entry, just make a new .desktop file in here.
* You can use %F and %f in exec argument to specify the path
