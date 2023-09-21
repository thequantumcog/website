---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
description: "Desc Text."
url: "/{{ .Name | lower }}/"
# cover:
#     image: "<image path/url>"
#     alt: "<alt text>"
#     caption: "<text>"
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
draft: true
---

