---

copyright:
  years: 2021，2021
lastupdated: "2021-09-15"

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

# Bringing your own data to virtual server instance with cloud tape connector - Draft
{: #vsi-is-ctc}

You can use cloud tape connector (CTC) to backup data sets from on prem to z/OS virtual server instance. On the z/OS virtual server instance, you can further develop and test data sets.
{: shortdesc}

## Before you begin

Complete the following prerequisites:

1. Make sure that you have created a z/OS virtual server instance in the Virtual Private Cloud (VPC) environment and the instance is accessible via 3270 connection. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers) and [Connecting to z/OS instances](/docs/vpc?topic=vpc-vsi_is_connecting_zos)

2. Make sure that you can edit the z/OS virtual server instance via the IBM Cloud console. For more information, see [Managing virtual server instances](docs/vpc?topic=vpc-managing-virtual-server-instances&interface=ui)

3. Create Cloud Object Storage instance (COS) and a service credential for accessing the instance/bucket. Additionally, obtain the IP address of the cloud object storage public endpoint via ping. For more information, see [creating cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
--这个credential for accessing the bucket 没有找到

4. Make sure that you have created the bucket to store your data sets. For more information, see [Creating buckets in Cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets)   ---这个页面有点outdated

???Allowing public access: https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access???

## Backing up data to cloud object storage:

After you create the cloud object storage (COS), bucket and prerequisites, complete the following steps to back up data set to cloud object storage.

1. Install the Cloud tape connector on the On-prem LPAR. For more information, see [Configuration Cloud tape connector](https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=connector-configuration-summary)
---这里有没有需要和dev确认的 Cloud specific --Scerario specific？

2. Create the partitioned data set and give the name for the partition data set. For more information, see[Creating partition data set](https://www.ibm.com/docs/en/zos/2.4.0?topic=ispfpdf-creating-partitioned-data-set).

The name of the partition data set must be unique.
{: important}
--这一步不是非常的确定，自己没有test过

3. Dump the partition data set into sequential data set via the ISPF(2.3).
   1. Enter the `%CUZVP11` command and bring up to the ISPF panel once you have installed the cloud tape connector. you need to click `3. Cloud datasets` and find the partition data set that you have created. For example, you can see the following panel.

   ```
   1. Cloud connector settings
   2. cloud server status
   3. Cloud datasets
   4. Backup History datasets
   5. Acruve Tasks
   X. Exit
   ```
{: screen}

   2. Enter the `b` command to browse the data set and find multiple data sets within the partition data set.

   3. On the top side, Enter `l dump` command to dump the partition data set into sequential data sets. For example, you can find

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
   ```
   {: Screen}
   5. TERSE command
   ```
   000023 TERSE EXEC PGH*TRSMAIN
   ```
   6. SYSUT2 command
   ```
   000031 //STSUT2 XX DSN*YOURDATASETNAME.JCL.TERSE
   ```
   {: Screen}
   And on the command `RES` and then `SUBMIT`

   Verify the sequential data has been created via the ISPF. If you enter `YOURDATASETNAME.JCL` next to the Dsname Level, you should also find the corresponding sequential data set named: `YOURDATASETNAME.JCL.TERSE`

4. Verify the data set in the cloud object storage. Now If you enter the `%CUZVP11` command and verify the cloud tape connector via `3. Cloud Datasets`, the data set is backed up in the cloud tape connector. The cloud data set name is the same as in the Cloud object storage. For exmple, you can check here.
```
Dataset Name                 Backup Timestamp        Cloud Dataset name
YOURDATASETNAME.JCL.TERSE         XXXXX              CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX
```
{: Screen}


Because the Cloud tape connector configure with Back up filter criteria with certain file name/type, and once it filters the certain files, it would write to the Cloud object storage instance. 
Each Cloud tape connector also has its own CTC repository and use it to keep track of what has been back up on the COS.  (这两段不知道放在哪里比较合适)
 

## Verifing data set in the cloud object storage bucket

Now, in your cloud object storage bucket, you should find 2 automatic object data sets. one is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXX` and the other is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX.1INFOCTC`
The first one is the meta data set and it is the identifier for the Rebuild Job to discover data sets between the Cloud object storage and z/OS Virtual server instance.

---这里kevin说了多的这个meta data, client have to run on the target side and need to check (How?)


## Restoring data on virtual server instance side:

After you back up data to the cloud object storage, complete the following steps to restore data set on z/OS virtual server instance side.

1. Enter cloud tape connector parameter `%CUZVP11` command and click `2 cloud server status` to check the repository name and verify the name, if you currently would like to find the JCL data in the  virtual server instance, it would show `No data names found` on the top right corner.
---这里CUZDATA 的话，之前有出现z/OS repository的方面嘛，这里就要确认是在CUZDATA （same repositroy)?

2. Restore the data set via cloud tape connector.

   1. On the Dsname level and use `IBMUSER.JCL` to discover the data sets and enter `b` to browse the `CUZJRBLR` rebuild job, and then enter `SUBMIT` on the bottom.  

   2. Check the `3. Cloud datasets` and find the sequential data set `YOURDATASETNAME.JCL.TERSE`, Enter`R` command to restore the data sets.

   3. Delete the bucket on the `Restore to Alias` and change `Restore Dataset` to be `Y`

   4. You need to browse the `IBMUSER.JCL` by input `b` on `Restor` and find the example below:
   ```
   //INFILE DD DISP=SHR,DSN=YOURDATASETNAME.JCL.TERSE
   //OUTFILE DD DISP=SHR,DSN=&&TEMP1
   *
   //RESTORE EXEC PGM=ADRDSSU,COND = (0,NE)
   ```
   {: Screen}

   To submit the restoring job, then enter `SUBMIT` command on the bottom command line

3. Verify data set on virtual server instance and back to the Dsname level, input `YOURDATASETNAME.JCL` and you could find `YOURDATASETNAME.JCL.TERSE` sequential data set on the virtual server instance side.


Can create a report before touching the repository ----这个需要问一下


![BYOD using cloud tape connector](images/vpc-byod-ctc.svg "Figure showing BYOD using cloud tape connector"){: caption="Figure 1. BYOD using cloud tape connector" caption-side="top"}

Then use cloud tape connector to restore JCL data set from COS and `SUBMIT`
You can now find your partition data set on virtual server instance side and verify the existence.
