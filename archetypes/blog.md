---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
description: ''
author: 'Darius Weber'
date: {{ .Date }}
tags:

layout: "single"
socialShare: false
outputs:
    - HTML
    - RSS

draft: true
---
