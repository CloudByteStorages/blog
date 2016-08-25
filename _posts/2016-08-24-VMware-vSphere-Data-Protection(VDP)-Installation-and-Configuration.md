---
layout:     post
title:      VMware vSphere Data Protection(VDP) Installation and Configuration
subtitle:   "[ VMWARE SETUP ]"
categories: [general, setup, vmware, vdp]
tags:       [vmware, setup]
date:       2016-08-24 12:30:00 (UTC +5:30)
contributor_name:     Abhishek Shrivastava
contributor_image:    "abhishek.jpg"
contributor_linkedin: abhishek-shrivastava-03921390
contributor_emailid:  abhishek@cloudbyte.com
---

# VMware vSphere Data Protection(VDP)

- VMware vSphere Data Protection is a backup and recovery solution from VMware. 
- Fully integrated with VMware vCenter Server and VMware vSphere Web Client, providing disk-based backup of virtual machines and applications.
- vSphere Data Protection is based on the industry-leading EMC Avamar deduplication backup and recovery software.

## Prerequisites for VMware vSphere Data Protection(VDP)

- Before installing VDP you need to make sure that your VMware Vcenter and the ESX hosts **_NTP servers_** are synced with the same DNS server,
  which is to be used by the VDP.
  
## Installing VMware vSphere Data Protection(VDP)

- Download the OVA template from 

  ```http
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

## Configuration of VDP - PART I

- After the deployment is done and the VDP VM is powered on, the first step will be configuring the timezone.

  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image3.PNG)

- Once the above is done SSH into the system using **_root_** as username and **_changeme_** as the password. 

- We will then need to update **_/etc/hosts_** to reflect the IP Address/Hostname of our VDP appliance as well as 
  any others you may want VDP to be able to resolve. 

- It should look something like this:
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image4.PNG)

- Now add the following highighted part in **_/etc/reslov.conf_**:
  
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image5.PNG)

- Next we need to edit the dnsmasq configuration file located in **_/etc/dnsmasq.conf_** and add the following 
  entry (replace it with the IP Address you have assigned your VDP appliance):

  ```
  server=20.10.112.131
  ```
- Finally we just need to start the dnsmasq service as well as enable it to automatically startup on boot by 
  running the following two commands:

  ```
  /etc/init.d/dnsmasq start
  chkconfig dnsmasq on
  ```
- To confirm that everything has been configured correctly, we will perform both a forward and reverse lookup of 
  our VDP hostname and IP Address. You can do so by using **_nslookup_** command or any others such as dig or host. 
  In this example, I will be using nslookup and you will need to run the following two commands (ensure to replace 
  it with your hostname/IP Address):

  ```
  nslookup vdp.vmcert.com
  nslookup 20.10.112.131
  ```
  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image6.PNG)

- Once you have confirmed both forward and reverse lookups are successful, you can then proceed to configuring your 
  VDP appliance by opening a browser to **_https://[VDP-ADDRESS]:8543/vdp-configure_** and proceed with moving forward 
  with the VDP configuration wizard.
  
  ``` 
  Note: 
  - Ensure that 127.0.0.1 is shown in the VDP configuration UI for the DNS entry. 
  - For hostname, you will need to use the short hostname even though a hostname is officially defined as specifying the FQDN
  ```

## Configuration of VDP - PART II

- STEP 1: Network Settings
  - By default your Stactic IP, Netmask, Gateway and Primary DNS will be present in the settings page.
  - Make sure your Primary DNS is **_127.0.0.1_**, if so proceed further.
  - Enter the Hostname and Domain you provided in **_/etc/hosts_**.

  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image7.PNG)

- STEP 2: Setting Up Timezone
  - Select the timezone according to your region and then proceed further.

- STEP 3: Updating VDP Credentials
  - Update the VDP password with you credentials.

  ![alt text](https://raw.githubusercontent.com/CloudByteStorages/blog/gh-pages/post_images/vdp_image8.PNG)


