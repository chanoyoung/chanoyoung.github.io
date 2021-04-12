---
date: 2020-01-20 19:46
layout: post
title: MySQL] IFNULL, NULLIF
subtitle:
description:
image:
category: programming
tags:
 - sql
author: chanoyoung
---

## IFNULL
```sql
IFNULL(expr1, expr2)
```
- expr1이 NULL이면 expr2를 리턴하고, NULL이 아니면 expr1을 리턴한다.

## NULLIF
```sql
NULLIF(expr1, expr2)
```
- expr1 = expr2가 True이면 NULL을 리턴하고, 그렇지 않으면 expr1을 리턴한다.

```sql
CASE WHEN expr1 = expr2 THEN NULL
     ELSE expr1 END
```
- 위의 식과 동일한 기능을 한다.
