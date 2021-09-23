---

copyright:
  years: 2021，2021
lastupdated: "2021-09-23"

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
{:experimental: .experimental}
{:table: .aria-labeledby="caption"}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Bringing your own data to z/OS virtual server instance  - Draft
{: #vsi-is-ctc}

You can back up data sets from on-prem z/OS operating system via using cloud tape connector and then restore it to the z/OS virtual server instance in the cloud. The following diagram gives you an overview of steps you need to take to bring the data set from z/OS on-prem to z/OS virtual server instance.
{: shortdesc}

Working with z/OS virtual server instances on VPC is an experimental feature that requires special approval. Contact your IBM Sales representative if you're interested in getting access.
{: experimental}

![BYOD to z/OS virtual server instance](images/vpc-byod-ctc.svg "Figure showing BYOD to z/OS virtual server instance"){: caption="Figure 1. BYOD to z/OS virtual server instance" caption-side="bottom"}

 The whole process is divided into 3 main parts. Firstly, you can back up partition data set to the cloud tape connector on the on-prem z/OS . Then you can synchronize cloud tape connector repositories via the Rebuild Job (CUZJRBLR). This rebuild job will discover the meta data on the cloud object storage and then rebuild the data set to the z/OS virtual server instance repository. Lastly, you can restore data set on the z/OS virtual server instance. You can now perform following steps.

## Before you begin

Complete the following prerequisites:

1. Make sure that you have created a z/OS virtual server instance in the Virtual Private Cloud (VPC) environment and the instance is accessible via 3270 connection. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers) and [Connecting to z/OS instances](/docs/vpc?topic=vpc-vsi_is_connecting_zos).

2. Make sure that you have created the Cloud Object storage. For more information, see [Creating cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

3. Make sure that you have created the bucket to store your data sets. For more information, see [Creating buckets in Cloud object storage](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets).

4. Make sure that you have access to the bucket level and service credential. For more information, see [Manage access](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-administrators#administrators-manage-access).

5. Make sure that you have obtained the IP address of the cloud object storage public endpoint via ping. For more information, see [Allowing public access](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access).
[To do: What would be the correct IP address access reference]
[To do: which cloud server type to use and need confirmation: Which cloud server type to use and need confirmation https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=options-create-cloud-server-definition]


## Backing up data set to cloud object storage

 Complete the following steps to back up data set from z/OS to the bucket of the cloud object storage.

1. Install the Cloud tape connector on the on-prem z/OS instance. For more information, see [Configuration Cloud tape connector](https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=connector-configuration-summary). [To do: Whether there is any z/OS on-prem specific configurations need to notice here]

2. Prepare the partiton data set that you want to back up. For example, the partition data set name is `IBMCTCTEST.JCL`.


3. Back up z/OS on-prem data sets to cloud object storage via cloud tape connector interface.
   1. Enter the `%CUZVP11` command to bring up the cloud tape connector ISPF interface.

   2. Select `3. Cloud datasets` and find the partition data set that you want to back up. You can also enter `b` command to browse your current data set.

   3. Update your JCL to include the following statements. This process will dump the partition data sets into sequential data sets and pack the data sets to the z/OS cloud tape connector with specified destination name. [To do: Not sure whether the DUMPTRS.JCL is the only solution https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=interface-staging-options Here is the link for CTC menu ]

    ```
    // DUMP DATASET(INCLUDE(IBMCTCTEST.JCL))
    ...
    // TERSE EXEC PGM=TRSMAIN.PARM='PACK',COND = (0.NE)
    ...
    // SYSUT2 DO DSN=IBMCTCTEST.JCL.TERSE,
    ...
    ```
    {: screen}

    where:
    * `IBMCTCTEST.JCL`is the partition data set you selected to dump.
    * `IBMCTCTEST.JCL.TERSE` is the destination data set name to the cloud object storage.


   4. To submit the back up job, enter the `SUBMIT` command.

   5. Verify the sequential data set has been created via the ISPF (3.4). If you enter `IBMCTCTEST.JCL` next to the Dsname Level, the target data set `IBMCTCTEST.JCL.TERSE` is also available.

4. You can verify the data set in the cloud object storage in either of the following approaches:

   * On ISPF: Enter the `%CUZVP11` command to bring up the cloud tape connector interface and select `3. Cloud Datasets`, the data set is backed up in the cloud tape connector. The cloud data set name is the same as in the Cloud object storage. For example, you can see the similar results on your screen. The data set `IBMCTCTEST.JCL.TERSE` is copied to the cloud object storage with the staging alias `CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX`.
    ```
    Dataset Name                 Backup Timestamp        Cloud Dataset name
    IBMCTCTEST.JCL.TERSE         XXXXX              CUZSTAGE.DUMPTRS.JOBXXXX.SYSUT2.XXXXXXXX
    ```
    {: screen}

   * On the object storage resource instance: Enter the bucket and you will find repository records of the data set. For more information, see [Repository records](https://www.ibm.com/docs/en/cloud-tape-connector/2.1?topic=repository-records).


## Synchronizing cloud tape connector repositories

You need to run Rebuild job (CUZJRBLR) on the z/OS VSI, so that the cloud tape connector on the z/OS VSI can discover data sets in cloud object storage backed up from the previous step.
1. Connect the cloud object storage to the z/OS virtual server instance. Check the cloud server status on ISPF (2) and confirm the same repository.

2. Discover Rebuild Job via ISPF. On the ISPF, enter `IBMUSER.JCL` on the Dsname level line to discover the data sets and enter `b` command to browse the `CUZJRBLR` rebuild job. To submit the job, enter `SUBMIT` command on the bottom command line.


## Restoring data to the z/OS virtual server instance

Complete the following steps to restore data set on z/OS virtual server instance.

1.  Click the ISPF `3. Cloud datasets` and find the sequential data set `IBMCTCTEST.JCL.TERSE`. Then enter `R` command to restore the data sets.

2.  Delete the bucket name on the `Restore to Alias` line and change `Restore Dataset` to be `Y`.

3.  You can now update the data set you want to restore in the `IBMUSER.JCL`. This process will  unpack the sequential data set and restore it to the z/OS virtual server instance.
    ```
    ...
    //UNTERSE EXEC PGM = TRSMAIN,PARM='UNPACK'
    //INFILE DD DISP=SHR,DSN=IBMCTCTEST.JCL.TERSE
    ...
    //RESTORE EXEC PGM=ADRDSSU,COND = (0,NE)
    ```
    {: screen}

    where `IBMCTCTEST.JCL.TERSE` is the destination data set name to the z/OS virtual server instances.

4. To submit the restoring job, then enter `SUBMIT` command.

5. Verify partition data set on z/OS virtual server instance. You can open the cloud tape connector interface and enter `IBMCTCTEST.JCL` command on Dsname level, then you can find both sequential data set (`IBMCTCTEST.JCL.TERSE`) and partition data set (`IBMCTCTEST.JCL`) together on the virtual server instance.
