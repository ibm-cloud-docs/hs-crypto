---

copyright:
  years: 2021
lastupdated: "2021-09-13"

keywords: CTC，cloud tape connector

subcollection: vpc

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
{: #vsi_is_ctc}

You can use cloud tape connector (CTC) to backup data sets from on prem to z/OS virtual server instance. On the z/OS virtual server instance, you can further develop and test data sets.
{: shortdesc}

## Before you begin
{: #Before_ctc_XXX}

Complete the following prerequisites:

1. Make sure that you have created a z/OS virtual server instance in the Virtual Private Cloud (VPC) environment and the instance is accessible via 3270 connection. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers) and [Connecting to z/OS instances](/docs/vpc?topic=vpc-vsi_is_connecting_zos)

2. Make sure that you can edit the z/OS virtual server instance via the IBM Cloud console. For more information, see [Managing virtual server instances](docs/vpc?topic=vpc-managing-virtual-server-instances&interface=ui)

3. Create Cloud Object Storage instance (COS) and a service credential for accessing the instance/bucket. Additionally, obtain the IP address of the cloud object storage public endpoint via ping. For more information, see [creating cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

4. Make sure that you have created the bucket to store your data sets. For more information, see [Creating buckets in Cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets)   ---这个页面有点outdated

???Allowing public access: https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access???

## Backing up data to cloud object storage:

After you create the cloud object storage (COS), bucket and prerequisites, please complete the following steps to back up data set to cloud object storage.

1. Install the Cloud tape connector on the On-prem LPAR and see [Configuration Cloud tape connector](https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=connector-configuration-summary)---这里有没有需要和dev确认的 Cloud specific --Scerario specific？

2. 2个multiple data set怎么打包到Partition data set的过程？？？

Once you are in ISPF panel, you need to go to `3. Cloud datasets` and find the partition data set you have created. The name should be unique and include multiple JCL data sets.

A primary use of ISPF is to create and manipulate PDS data sets. These data
sets typically consist of source code for programs, text for manuals or help
screens, or JCL to allocate data sets and run programs.

For example,

```
1. Cloud connector settings
2. cloud server status
3. Cloud datasets
4. Backup History datasets
5. Acruve Tasks
X. Exit
```
{: screen}

You can press `b` to browse the data set and find multiple JCL data sets.

3. On the top side, Command `l dump` and then on the DUMPTRS command `v`, you would get interface like:

```
000001 // DUMPTRS
000002 //
000003 //DUMP
000004 //DASD
```
{: Screen}
And on the command `RES` and then `SUBMIT`

Once the dump data is been submitted, on the 'Dsname Level' and input CTCTEST.JCL, you would find the corresponding sequential data set named: `CTCTEST.JCL.TERSE`
Dump PDS containing some JCL members to sequential, tersed data set.

4. After you input 'SUBMIT' on ISPF panel, it would generate the data set with 'CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXX', This data set number is the same as in the Cloud object storage.
```
Dataset Name         Backup Timestamp        Cloud Dataset name
CTCTEST.JCL.TERSE         XXXXX              CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX
```
{: Screen}
Because the Cloud tape connector configure with Back up filter criteria with certain file name/type, and once it filters the certain files, it would write to the Cloud object storage instance. 
Each Cloud tape connector also has its own CTC repository and use it to keep track of what has been back up on the COS. 
Dump JCL - INFILE/INFILE/OUTFILE/RESTORE） 

## Verifing data set in the cloud object storage bucket

1. Now, in your cloud object storage bucket, you would find 2 automatic object data sets. one is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXX` and the other is `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX.1INFOCTC`
The second one is the meta data set and it is the identifier for the Rebuild Job to discovery between the Cloud object storage and z/OS Virtual server instance.


## Restoring data on virtual server instance side:

Now we back to the ISPF (3.2) and press `%CUZVP11` and choose `2 cloud server status` to check in the same repository `CUZDATA`, if you currently would like to find the JCL data in the Virtual server instance, it would show `No data names found` on the top right corner.

1. On the Dsname level and use `IBMUSER.JCL` to discover the data sets and browser the `CUZJRBLR`, and input `SUBMIT` on the bottom.  

2. Check the `3. CLoud datasets` and find the sequential data set `CTCTEST.JCL.TERSE`, command `R`to restore the data sets.

3. Delete the bucket on the `Restore to Alias` and `Restore Dataset` to be `Y`

4. After restoring and back to the Dsname level, you could find CTCTEST.JCL.TERSE job on the virtual server instance side.

5. You need to browse the `IBMUSER.JCL` first by input `b` on `Restor`and find the example below:
```
//INFILE DD DISP=SHR,DSN=CTCTEST.JCL.TERSE
//OUTFILE DD DISP=SHR,DSN=&&TEMP1
*
//RESTORE EXEC PGM=ADRDSSU,COND = (0,NE)
```
{: Screen}
Then on the Command line, input `SUBMIT`
Back to ISPF and run the JCL job to do the discovery (Basically the CTCTEST.JCL is not on the VSI side)  
IBMUSER.JCL is all the JCL jobs exist on the VSI side and you could check the existence. 

Can create a report before touching the repository

Then use cloud tape connector to restore JCL data set from COS and `SUBMIT`
You can now find your partition data set on virtual server instance side and verify the existence.
