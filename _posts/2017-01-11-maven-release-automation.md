---
layout: post
title:  "Maven Release Automation"
date:   2017-01-11 14:41:00 -0800
author: "Jianghao Lu"
comments: true
---

## Current release process
1. Build jars
2. Sign jars using Jenkins (corpnet required)
3. Move them into a correct file structure
4. Deploy to staging using Jenkins (corpnet required)
5. Test
6. Click "Release" on UI

## New steps for properly configured GitHub repos
1. run Jenkins job - select packages to release

## New steps for any Maven project
1. Build jars
2. Move jars and poms into a correct file structure
3. Deploy to staging using Jenkins

## Things to do
- [ ] Write a script that signs the jars from anywhere on signing machine
- [ ] Replace publishig job with a new one that runs the script first
- [ ] Write a script that promotes a staging repo to release
