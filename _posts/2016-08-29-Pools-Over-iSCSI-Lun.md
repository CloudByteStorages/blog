---
layout:     post
title:      Pools Over iSCSI Lun
subtitle:   "[ CONFIGURATION ]"
categories: [general, setup, configuration]
tags:       [elasticenter, setup]
date:       2016-08-29 17:30:00 (UTC +5:30)
contributor_name:     Abhishek Shrivastava
contributor_image:    "abhishek.jpg"
contributor_linkedin: abhishek-shrivastava-03921390
contributor_emailid:  abhishek@cloudbyte.com
---

# Introduction

  In ElastiCenter to create an extra Pool in a particular NODE, we have to perform either one of these:
  
  - Adding a JBOD to that NODE, or
  - Adding additional disks to the JBOD already attached to the NODE.
  
  But what if 
  
  - We don't have an extra JBOD, or 
  - The JBOD is been used in some another ElastiCenter or 
  - We don't have extra Disks for the JBOD.
  
  In that case we either had to purchase extra disks or a new JBOD itself which might be a bit costly. But what if 
  I say that we do not have to do any of these and still we can create a Pool for your node. Want to know how, lets find out.
  
# Pools over iSCSI Lun

  In ElastiCenter 2.0.0 we have a feature that use  
