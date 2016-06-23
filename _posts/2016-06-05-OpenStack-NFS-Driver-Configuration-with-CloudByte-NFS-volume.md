---
layout:     post
title:      OpenStack NFS Driver Configuration with CloudByte NFS volume
subtitle:   "[ OPENSTACK SETUP ]"
categories: [general, setup, openstack]
tags:       [openstack, setup]
date:       2016-06-05 11:30:00 (UTC +5:30)
contributor_name:     Abhishek Shrivastava
contributor_image:    "abhishek.jpg"
contributor_linkedin: abhishek-shrivastava-03921390
contributor_emailid:  abhishek@cloudbyte.com
---

# Introduction

  The Network File System (NFS) is a distributed file system protocol originally developed by Sun Microsystems in 1984. An NFS server
  exports one or more of its file systems, known as shares. An NFS client can mount these exported shares on its own file system. You 
  can perform file actions on this mounted remote file system as if the file system were local.

### NFS driver notes

- cinder-volume manages the mounting of the NFS shares as well as volume creation on the shares. Keep this in mind when planning your
  OpenStack architecture. If you have one master NFS server, it might make sense to only have one cinder-volume service to handle all
  requests to that NFS server. However, if that single server is unable to handle all requests, more than one cinder-volume service is
  needed as well as potentially more than one NFS server.

- Because data is stored in a file and not actually on a block storage device, you might not see the same IO performance as you would 
  with a traditional block storage driver. Please test accordingly.

- Despite possible IO performance loss, having volume data stored in a file might be beneficial. For example, backing up volumes can be as easy as copying the volume files.

### Options supported by OpenStack NFS driver
  
  ```
  | Configuration option = Default value     | Description                                                                          | 
  | [DEFAULT]                                |                                                                                      |
  | ---------------------------------------- |:------------------------------------------------------------------------------------:| 
  |  nfs_mount_attempts = 3                  | (IntOpt) The number of attempts to mount nfs shares before raising an error. At least                                            one attempt will be made to mount an nfs share, regardless of the value specified.    |
  ```
  
# Configuration steps 

In order to configure the CloudByte NFS volume against OpenStack NFS driver we need to create and discover the NFS volume from CloudByte first:

- Firstly create a NFS volume in CloudByte ElastiStor with some good specifictions. For eg, 20 GB.
- Set the **NFS client configuration** so that it can point to OpenStack setup machine.
- Now go to the OpenStack setup and run the **showmount -e <VSM_IP>** command to see the NFS export list. (It should show the NFS volume we created)

After the creation and discovery of NFS volume is done proceed wit the following steps to use this volume with OpenStack NFS driver:

- Create a file , lets say **/etc/cicnder/cb_nfs_shares**, and insert the NFS volume details
  ```
  For eg : 172.16.19.20:/ACC1TEST
  ```
- Now we need to add a new backend in **cinder.conf** that will point to OpenStack NFS driver.
- It will also use the **cb_nfs_shares** to access the NFS volume form CloudByte.
  ```
  # vi /etc/cinder/cinder.conf
  
  [DEFAULT]
  default_volume_type = cb-nfs
  enabled_backends = cloudbyte-nfs
  
  [cloudbyte-nfs]
  nfs_shares_config = /etc/cinder/cb_nfs_shares
  volume_driver = cinder.volume.drivers.nfs.NfsDriver
  volume_backend_name = cloudbyte-nfs
  nfs_mount_options=vers = 3
  nfs_mount_point_base = $state_path/mnt
  ```