---
layout:     post
title:      VMware vSphere Data Protection(VDP) Instalation and Configuration
subtitle:   "[ VMWARE SETUP ]"
categories: [general, setup, vmware, vdp]
tags:       [vmware, setup]
date:       2016-08-22 17:30:00 (UTC +5:30)
contributor_name:     Abhishek Shrivastava
contributor_image:    "abhishek.jpg"
contributor_linkedin: abhishek-shrivastava-03921390
contributor_emailid:  abhishek@cloudbyte.com
---

# VMware vSphere Data Protection(VDP)

  VMware vSphere Data Protection is a backup and recovery solution from VMware. It is fully integrated with VMware vCenter Server and
  VMware vSphere Web Client, providing disk-based backup of virtual machines and applications. vSphere Data Protection is based on the
  industry-leading EMC Avamar deduplication backup and recovery software.
  
## Installing VMware vSphere Data Protection(VDP)

- Download the OVA template from 

  ```link
  https://my.vmware.com/web/vmware/details?downloadGroup=VDP61&productId=491
  ```

- Deploy the OVA template on a VCenter.

- While deploying select the Datastore (of size atleast 2TB), on top of which you want to deploy the VDP VM.

  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image1.PNG)

  NOTE: In this case the Datastore seelcted is a CloudByte Volume mounted on the ESX host.

- Now after couple of steps, use the following as the initial Network configuration for VDP VM.
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image2.PNG)

- The deployment will take around 20-25 minutes to complete.

- Once the deployement is done, the next steps will involve the configuration of VDP.



