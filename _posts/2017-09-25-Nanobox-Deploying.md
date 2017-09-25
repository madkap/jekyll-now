---
layout: post
title: Nanobox and Rails 
description: General notes for Nanobox and Rails
tags: nanobox notes rails
---

## Steps for deploying to Nanobox
Unique situation because I am constantly seeding since I haven't builted a CMS yet.
```
nanobox deploy dry-run
nanobox console dry-run web.mian
sudo sv stop puma
rake db:reset
sudo sv start puma
```

## Set up remote environments
```
nanobox remote rm default
nanobox remote add base10 producton
nanobox remote add base10-staging
 ```
 
