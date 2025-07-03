---
title: "Regex Cheatsheat"
date: 2025-06-30T13:10:45+05:00
description: "Desc Text."
url: "/regex-cheatsheat/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: true
---

^ $ are same as vim (start/end)

[] match char (can be used as or)

[^] donot match this (i.e match all except this)

. match a char i.e [a-zA-Z0-9] including symbols and space

\* wildcard
+ less wildcard e.g c.*t will match "ct", "cat" and "cat and bat" but c.+t will only match "cat"  and "cat and bat" 
? optional meaning be less strict about it. [T]?he will match "The" and "he"
{} specify range e.g [0-9]{2,3} -> 2 is min -> 3 is max will match 192 and 1928 but i will not match the 9 in 19289

