---
layout: default
title: Get XP
parent: User Data
nav_order: 5
nav_exclude: false
description: "Get xp information"
permalink: docs/user-data/get-xp
---
# Layout Utilities
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## End-Point

<br/>

```
https://api.shockmc.it/v1/userdata/getxp
```


| Method           | Allowed                       |
|:-----------------|:------------------------------|
| `GET`            | `✅`                          |
| `POST`           | `✅`                          |

<br/>

## Request json data 

<br/>

The request must have the following data or the request will fail.

```json
{
    "username": "player's username"
}
```

Username must match the following REGEX or the request will fail. ```[a-zA-Z0-9_]{1,16}```

<br/>

## Request response

<br/>

#### Response if the request has invalid data or username

```json
{
    "error": true,
    "description": "Invalid data or invalid username."
}
```

<br/>

#### Response if the user never joined the server

```json
{
    "error": true,
    "description": "Userdata not found."
}
```

<br/>

#### Response if success

```json
{
    "error": "false",
    "description": "",
    "username": "", # Username of the user
    "role": "", # Rank of the user
    "xp": 0 # Experience of the user
}
```