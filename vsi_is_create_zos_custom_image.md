---

copyright:
  years: 2021
lastupdated: "2021-08-11"

keywords: creating a z/OS custom image for vpc, cloud-init, qcow2

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}

# Creating a z/OS custom image - DRAFT
{: #create-zos-custom-image}

You can create your own custom z/OS-based image to deploy a virtual server instance in the {{site.data.keyword.vpc_full}} infrastructure.
{: shortdesc}

Your image must adhere to the following custom image requirements:
* Contains a single file or volume
* Is cloud-init enabled
* Compressed size doesn't exceed 85 GB because the boot image in the {{site.data.keyword.vpc_short}} is limited to 100 GB

## Before you begin
{: #before-creating-zos-custom-image}

1. Make sure that you download, install, and initialize the following CLI plug-ins:
    * {{site.data.keyword.cloud_notm}} CLI
    * The infrastructure-service plug-in
    For more information, see [Setting up your API and CLI environment](/docs/vpc?topic=vpc-set-up-environment#cli-prerequisites-setup).

2. Make sure that you already [created a VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-cli).

3. Make sure that you have the `prepare-z-cloud-image.sh` script and the z/OS cloud base image.

4. Make sure that an on-premises z/OS guest system is installed through the IBM System z Personal Development Tool (zPDT), and create backups for the CKD image files and `devmap` file on the z/OS guest system. For more information, see [IBM zPDT Guide and Reference](https://www.redbooks.ibm.com/redbooks/pdfs/sg248205.pdf){: external}.

5. Make sure that the z/OS guest system meets the following network requirements.

   * TCP/IP Address: Only the default tunnel IP address of `10.1.1.1` is supported. Therefore, the TCP/IP address on the guest z/OS system needs to be an address on this network. You can configure `10.1.1.2` as the IP address.
   * TCP/IP Network Mask: An appropriate network mask that corresponds to the IP address must also be configured. Because virtual servers that are running in the {{site.data.keyword.vpc_short}} environment have other network interfaces that use `10.*` IP addresses, the network mask for the z/OS guest system needs to be 255.255.255.0. This address prevents unintended network interactions between the tunnel IP network and other network interfaces on the virtual server that also have `10.*`` IP addresses. An incorrect network mask in the guest might result in connectivity issues when it tries to reach the guest.
   * TCP/IP Component Status: The TCP/IP component must be started and running successfully in the z/OS guest system. If changes were made to the configuration as described in this document, then make sure that those changes were processed and TCP/IP components were restarted if necessary.

Complete the following steps to ensure that your own z/OS custom image can be successfully deployed in the
{{site.data.keyword.vpc_short}} infrastructure environment.

## Step 1 - Stop the guest z/OS system and zPDT
{: #stop-zos-guest}

 You can stop zPDT and the z/OS guest system through the zPDT console. From the **Instances** tab on the zPDT console, click the menu icon under the **Actions** column that corresponds with the instance to be stopped. Within the menu, select **Stop emulator**.


## Step 2 -  Update the `devmap` file corresponding to the z/OS system disk volume images
{: #update-devmap}

1. Log in as the user under which zPDT runs.  For example, `sudo su - ibmsys1`.

2. Go to the parent directory of the `volumes` directory. For example, `cd /home/ibmsys1/zdt`.

3. Create the `devmap` file in lowercase by copying the `aprof1` file. For example, `cp -p ./volumes/aprof1 ./volumes/devmap`. The target file name must be `devmap` so that it can be later recognized in the {{site.data.keyword.vpc_short}}.

4. Update the `[system]` section in the `devmap` to include the IPL statement. The IPL statement must be available in order for the z/OS system to boot automatically in the {{site.data.keyword.vpc_short}} as shown in the following example:

   ```
   [system]
   ...
   ipl 0a80 0A82AU  # Guest system from a zPDT environment
   ...
   ```
   {: pre}

5. Modify the `[manager]` section in the `devmap` to contain `/volumes` as the root directory in which the CKD files reside as shown in the following example:

   ```
   [manager]
   ...
   name awsckd 28
   device 0a80 3390 3990 /volumes/DMRES1
   device 0a81 3390 3990 /volumes/DMSYS2
   ...
   ```
   {: pre}

   The file names of the CKD files within the `device` statements must be uppercase.
   {: important}

6. Ensure the osa device entries in the `devmap` file have the same format as in the following example:

   ```
   device 400 osa osa --unitadd=0
   ```
   {: pre}

7. Review the changes to the `devmap` file by using the zPDT `awsckmap` utility as shown in the following example:

   ```
   awsckmap /home/ibmsys1/zdt/volumes/devmap
   ```
   {: pre}

## Step 3 - Create the compressed z/OS volume disk images and corresponding devmap
{: #create-zos-volume-images-tar}

1. Create the compressed the z/OS disk image files by using the following example command. The command iterates over all disk image files in the `volumes` directory (file names that contain uppercase letters and numbers) and compresses each of them into a .gzip file. The original disk image files are unchanged.

   ```
   for i in `find | grep  './volumes/^./[A-Z].*[A-Z 0-9]$'``; do gzip -vfk "$i"; done
   ```
   {: pre}

   This command might take a long time to complete depending on the number of disk image files and how large each file is.
   {: note}

2.  Compress the `devmap` file and the .gzip image file into a compressed file as shown in the following example:

    ```
    tar -zcvf zos-volumes.tar.gz ./volumes/*.gz ./volumes/devmap
    ```
    {: pre}

    If the compressed file is greater than 85 GB, the z/OS custom image fails to start in the {{site.data.keyword.vpc_short}}.
    {: important}

3. *Optional* Remove the compressed files that are under the `volumes` directory. For example, `rm ./volumes/*.gz`.

## Step 4 - Create the custom z/OS image by using the `prepare-z-cloud-image.sh` script.
{: #create-zos-custom-image-with-script}

1. Create separate directories for the cloud base image, the z/OS volume disk images, and the generated output images.

   ```
   mkdir base-cloud-images      # For the Cloud base image
   mkdir z-volume-images        # For the compressed z/OS volume disk images, the .tar file
   mkdir z-cloud-vsi-images     # For the generated custom z/OS image
   ```
   {: pre}

2. Copy the z/OS Cloud base image into the `/base-cloud-images` directory. For example, `mv z-vsi-image-base.qcow2 ./base-cloud-images`.

3. Copy the compressed z/OS volume file into the `/z-volume-images` directory. For example, `mv zos-volumes.tar.gz ./z-volume-images`.

4. Run the `prepare-z-cloud-image.sh` script to generate the z/OS custom image as shown in the following example:

   ```
   prepare-z-cloud-image.sh /base-cloud-images/z-vsi-image-base.qcow2 /z-volume-images /z-cloud-vsi-images/my-zos- vsi-image.qcow2
   ```
   {: pre}


## Step 5 - Upload image to {{site.data.keyword.cos_full_notm}}
{: #upload-zos-image-icos}

Upload your image to {{site.data.keyword.cos_full_notm}}. On the **Objects** page of your IBM Cloud Object Storage bucket, click **Upload**. You can use the Aspera high-speed transfer plug-in to upload images larger than 200 MB. For more information about uploading to {{site.data.keyword.cos_full_notm}}, see [Upload data](/docs/cloud-object-storage?topic=cloud-object-storage-upload).

## Next steps
{: #next-steps-creating-zos-image}

After your z/OS custom image is created, you can [import](/docs/vpc?topic=vpc-managing-images) it to VPC to provision images. Make sure that you have [Granted access to IBM Cloud Object Storage to import images](/docs/vpc?topic=vpc-object-storage-prereq).  
