---
layout:     post
title:      Setting up OpenStack CloudByte CI.
subtitle:   "[ OPENSTACK CLOUDBYTE CI SETUP ]"
categories: [general, setup, openstack, ci]
tags:       [openstack, setup, ci]
date:       2016-07-15 10:04:00 (UTC +5:30)
contributor_name:     Abhishek Shrivastava
contributor_image:    "abhishek.jpg"
contributor_linkedin: abhishek-shrivastava-03921390
contributor_emailid:  abhishek@cloudbyte.com
---

# What is OpenStack CI ?

OpenStack CI is a Continuous Integration Testing environment used to run the **tempest** test suite on each 
local changes a developer submits to **Gerrit** against any specific OpenStack upstream project. 
This patch code submitted then goes through a lot of reviews and CI tests then gets megered into the main OpenStack project repository.

## Why it is helpful ?

OpenStack CI is helpful in a lot of ways for developers by:

- Checking the stability of code.
- Helps in developing the code better.

## How to Setup a CI ?

For setting up a CI follow the instructions:

### Pre-requisites

#### Registering an Upstream Gerrit Account

- You will need to register a Gerrit account with the upstream OpenStack CI platform. 
- You can read the instructions for doing [that](http://ci.openstack.org/third_party.html#requesting-a-service-account).

#### Ensure Basic Packages on Hosts/VMs

- We will be installing a Jenkins master server and infrastructure on one host or virtual machine and one or more Jenkins slave servers on hosts or VMs.
- On each of these target nodes, you will want the base image to have the `wget`, `openssl`, `ssl-cert` and `ca-certificates` packages installed before running anything in this repository.

#### Set Up Your Data Repository 

- For more info on this refer [CloudByte-CI-Data](https://github.com/CloudByteStorages/CloudByte-CI-Data).
