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

  In **ElastiCenter 2.0.0** we have a feature that allows adding a iSCSI Luns to a NODE, which later used to create POOL.
  In order to do so we have a bunch of steps that need to be performed on **ElastiCenter 2.0.0**.

``` 
Note: 
- The following steps are performed using two different ElasriCenter setup.
- The iSCSI Lun from one of the ElastiCenter is used as a Disk in another ElastiCenter to create POOL.
```
  
### Configuration Steps
  
**STEP 1:**
  
- In Elasticenter, got to **HA Groups** section and click on Tasks action tab.
- In the dropdown you will get a list of tasks, select **Manage iSCSI Targets**.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi1.png)

**STEP 2:**
  
- In the iSCSI Targets page select the **Discover iSCSI Targets** option.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi2.png)

- Fill the **Target IP Address** and **Authentication Method** you want to use.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi3.png)

**STEP 3**
  
- Once the above step is done the iSCSI Lun will be added to the iSCSI Targets.
- Now connect to the iSCSI Lun in order to use it.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi4.png)

- You will get the following Job status after the iSCSI Target Lun is connected.

  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi5.png)
  
**STEP 4**

- Now go the the NODE, and check the newly added iSCSI Lun is showing in the **Shared Storage** section.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/pool_over_iscsi6.png)

- If the disk is shown as above then proceed with the creation of a POOL.
