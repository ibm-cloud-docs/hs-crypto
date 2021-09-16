---

copyright:
  years: 2021，2021
lastupdated: "2021-09-16"

keywords: CTC，cloud tape connector, cloud object storage

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:beta: .beta}
{:table: .aria-labeledby="caption"}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Bringing your own data to z/OS virtual server instance  - Draft
{: #vsi-is-ctc}

You can backup data sets from on prem z/OS operating system via using cloud tape connector and then restore it to z/OS virtual server instance in the cloud.
{: shortdesc}

## Before you begin

Complete the following prerequisites:

1. Make sure that you have created a z/OS virtual server instance in the Virtual Private Cloud (VPC) environment and the instance is accessible via 3270 connection. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers) and [Connecting to z/OS instances](/docs/vpc?topic=vpc-vsi_is_connecting_zos).


2. Make sure that you have created the Cloud Object storage. For more information, see [creating cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

3. Make sure that you have created the bucket to store your data sets. For more information, see [Creating buckets in Cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets).

4. Make sure that you have access to the bucket level and service credential. For more information, see [Manage access](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-administrators#administrators-manage-access).

5. Make sure that you have obtained the IP address of the cloud object storage public endpoint via ping. For more information, see [Allowing public access](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access).
--这个IP address 还是不大确认

--Which cloud server type to use and need confirmation (optional for now)
(Cloud server? https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=options-create-cloud-server-definition)


## Backing up data to cloud object storage:

 Complete the following steps to back up data set from the z/OS to the bucket of the cloud object storage.

1. Install the Cloud tape connector on the On-prem z/OS instance. For more information, see [Configuration Cloud tape connector](https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=connector-configuration-summary).
---这里有没有需要和dev确认的 Cloud specific --Scenario specific？(cloud 配置，每个字段的值，每个cloud的信息配置)

2. Prepare the partiton data set that you want to back up. For example, the partition data set name is `IBMCTCTEST.JCL`.


3.

Back up partition data set to cloud tape connector and back up to remote cloud object storage.

   1. Back up data  to cloud tape connector:  Enter the `%CUZVP11` command to bring up the cloud tape connector interface.

   2. Select panel once you have installed the cloud tape connector. you need to click `3. Cloud datasets` and find the partition data set that you want to back up. You can also enter `b` command to browse the data set and find multiple data sets within the partition data set.

   3. Enter `l dump` command to dump the partition data set into sequential data sets. For example, you can find


3ge statement
   ```
   000010 DUMP DATASER(INCLUDE(YOURDATASETNAME.JCL))
   ```
   {: Screen}
   4. Enter `v` command next to DUMPTRS, you would get interface like:

   ```
   000001 // DUMPTRS
   000002 //
   000003 //DUMP
   000004 //DASD
   ...
   000023 TERSE EXEC PGH*TRSMAIN
   ...
   000031 //STSUT2 XX DSN*IBMCTCTEST.JCL.TERSE
   ```
   {: Screen}

   `DUMPTRS` command means dump data from partition data set to sequential data sets.
   `TERSE` command means compress sequential data set
   `SYSUT2` statement is for output and authenticate SYSUT2 data set allocated with
    the destination to the cloud object storage.

   Enter `RES` command and then enter `SUBMIT` command on the bottom command line.
ISPF (3.4)
   7. Verify the sequential data has been created via the ISPF. If you enter `IBMCTCTEST.JCL` next to the Dsname Level, you should also find the corresponding sequential data set named: `IBMCTCTEST.JCL.TERSE`

4. Verify the data set in the cloud object storage. Now If you enter the `%CUZVP11` command and verify the cloud tape connector via `3. Cloud Datasets`, the data set is backed up in the cloud tape connector. The cloud data set name is the same as in the Cloud object storage. For exmple, you can check here.
```
Dataset Name                 Backup Timestamp        Cloud Dataset name
YOURDATASETNAME.JCL.TERSE         XXXXX              CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX
```
{: Screen}


Because the Cloud tape connector configure with Back up filter criteria with certain file name/type, and once it filters the certain files, it would write to the Cloud object storage instance. 
Each Cloud tape connector also has its own CTC repository and use it to keep track of what has been back up on the COS.  (这两段不知道放在哪里比较合适)
  下面的放上来

## Synchronize CTC repository

为什么要做 JCL CUZJRBLR --Synchronize
limitation
好处
CTC备份过去，repository meta data， repository

1. Cloud z/OS
2. JCL 找到

Now, in your cloud object storage bucket, you should find 2 automatic object data sets. one is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXX` and the other is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX.1INFOCTC`
The first one is the meta data set (不确定) and it is the identifier for the Rebuild Job to discover data sets between the cloud object storage and z/OS Virtual server instance.

---这里kevin说了多的这个meta data, client have to run on the target side and need to check (How?)


## Restoring data on virtual server instance side:

After you back up data to the cloud object storage, complete the following steps to restore data set on z/OS virtual server instance side.

1. Enter cloud tape connector parameter `%CUZVP11` command on top command line and click `2 cloud server status` to check the repository name. If you currently would like to find the `YOURDATASETNAME.JCL` data set in the  virtual server instance, it would show `No data names found` on the top right corner.
---这里CUZDATA 的话，之前有出现z/OS repository的方面嘛，这里就要确认是在CUZDATA （same repositroy)?

2. Restore the data set via cloud tape connector.

   1. Input `IBMUSER.JCL` on the Dsname level line to discover the data sets and enter `b` command to browse the `CUZJRBLR` rebuild job. To submit the job, then enter `SUBMIT` command on the bottom command line.  

   2. Check the `3. Cloud datasets` and find the sequential data set `YOURDATASETNAME.JCL.TERSE`. Then enter `R` command to restore the data sets.

   3. Delete the bucket name on the `Restore to Alias` line and change `Restore Dataset` to be `Y`

   4. You need to browse the `IBMUSER.JCL` by enter `b` command on `Restor` and find the example below:
   ```
   //UNTERSE EXEC PGM = TRSMAIN>PARM=UNPACK
   //INFILE DD DISP=SHR,DSN=YOURDATASETNAME.JCL.TERSE
   //OUTFILE DD DISP=SHR,DSN=&&TEMP1
   *
   //RESTORE EXEC PGM=ADRDSSU,COND = (0,NE)
   ```
   {: Screen}

   这三个解释一下

   To submit the restoring job, then enter `SUBMIT` command on the bottom command line.

3. Verify partiion data set on virtual server instance. You should back to the cloud tape connector page and enter `YOURDATASETNAME.JCL` command on Dsname level, you can find both sequential data set (`YOURDATASETNAME.JCL.TERSE`) and partition data set (`YOURDATASETNAME.JCL`) together on the virtual server instance side.

Can create a report before touching the repository --Parameter ----这个需要问一下


![BYOD using cloud tape connector](images/vpc-byod-ctc.svg "Figure showing BYOD using cloud tape connector"){: caption="Figure 1. BYOD using cloud tape connector" caption-side="top"}

Then use cloud tape connector to restore JCL data set from COS and `SUBMIT`
You can now find your partition data set on virtual server instance side and verify the existence.
