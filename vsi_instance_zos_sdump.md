---

copyright:
  years: 2021
lastupdated: "2021-08-12"

keywords: SDUMP, z/OS, storage, system dump, generation 2, gen 2

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

# Configuring additional SDUMP volumes for z/OS virtual server instances - DRAFT
{: #vsi_instance_zos_sdump}

You can add an additional volume to a z/OS virtual server instance and designate it as the SDUMP target. The system dump (SDUMP) is a dump of all the storage in the z/OS system that can be used for problem determination.

## Before you begin
{: #before_zos_sdump}

Complete the following prerequisites:

1. Make sure that you have created a z/OS virtual server instance in the Virtual Private Cloud (VPC) environment and the instance is accessible via 3270 connection. For more information, see [Creating virtual server instances](docs/vpc?topic=vpc-creating-virtual-servers) and [Connecting to z/OS instances](/docs/vpc?topic=vpc-vsi_is_connecting_zos).

2. Make sure that you can edit the z/OS virtual server instance via the IBM Cloud console. For more information, see [Managing virtual server instances](docs/vpc?topic=vpc-managing-virtual-server-instances&interface=ui).


## Adding the additional SDUMP volume
{: #vsi_instance_zos_add_sdump}

After you create your z/OS instance and complete the prerequisites, complete the following steps to add the additional SDUMP volume.

1. Attach a new block storage data volume to your z/OS virtual server instance. For more information, see [Attaching a block storage volume](/docs/vpc?topic=vpc-attaching-block-storage&interface=ui).

  If your z/OS virtual server instance is created by using the standard z/OS stock image, the size of the new block storage volume must not exceed 55 GB because the storage volumes larger than 55 GB are considered to be Extended Address Volumes (EAV) and cannot be used as the SDUMP target.  To work around this restriction and use larger volumes for SDUMP, you must run the command `SETSMS USEEAVZ(YES)` on the z/OS instance before you attach a larger block storage device for SDUMP.
  {: important}

2. Verify that the newly attached storage volume is ready to be used by the z/OS instance.

   Once the new storage volume is attached to the instance, a message is sent to the broadcast data set with the affected device address. For example:

   ```
   IKJ56455I IBMUSER LOGON IN PROGRESS AT 15:19:05 ON JUL
    Preparing attached block storage vde of size 55G    
    Attached block storage vde on address DD60           
   READY
   ```
   {: pre}

3. Initialize the volume via an ICKDSF job and vary it online.

  1. If your z/OS instance is not created by using the standard z/OS stock image, use ISPF (3.2) and create a new data set (for example, `IBMUSER.JCL`) to store the INITVOL JCL. For example, the data set can be created with the following settings:

       ```
       Space units . . . . . . TRKS
       Primary quantity. . . . 10
       Secondary quantity. . . 1
       Directory blocks. . . . 5
       Record format . . . . . FB
       Record length . . . . . 80
       Block size  . . . . . . 3120
       ```
       {: pre}

       If your z/OS instance is created by using the standard z/OS stock image, skip this step and consider using the existing `IBMUSER.JCL` data set for the JCL member to be created in the next step.
       {: important}

   2. Using ISPF (2 or 3.4), create a new data set member (INITVOL) with the following JCL that references the address of the new disk (eg. DD60).

       ```
       //INITVOL  JOB CLASS=A,MSGCLASS=H,MSGLEVEL=(1,1),NOTIFY=&SYSUID.,
       //         REGION=0M                                                  
       //STEP1    EXEC PGM=ICKDSF                         
       //SYSPRINT DD SYSOUT=*                                      
       //SYSIN    DD *                                             
       INIT UNITADDRESS(DD60) VOLID(SDUMP1) VERIFY(*NONE*) +
          VTOC(0,1,45) NODSEXIST
       /*
       ```
       {: pre}

       In this example, a `VOLID` of `SDUMP1` is used because `VOLID(SDUMP1)` is one of three volume IDs (SDUMP1, SDUMP2, and SDUMP3) that are pre-configured in the SDUMP settings on the standard z/OS stock image.

    3. To submit the job you are editing with the ISPF editor, first save any changes you made, then enter the `SUBMIT` command on the command line of the edit panel.

    4. Using ISPF (S or 13.14), open SDSF (Spool Search and Display Facility).

    5. Using SDSF (ST), view the status of jobs. An active job called `INITVOL` should be running and is currently waiting for confirmation to initialize the volume.

    6. Enter `s` next to the `INITVOL` job to view the job output log. Towards the bottom of the log, there is a prompt waiting for confirmation to initialize the volume.

    7. Using SDSF, reply to the prompt to confirm and initialize the volume. For example:

       ```
       /R 06, U
       ```
       {: pre}

       The INITVOL job should complete and no longer be an active job. Check the job log again to confirm that the job completed successfully.

    8. Using SDSF, vary online the new disk device based on the address. For example:

       ```
       /V DD60,ONLINE
       ```
       {: pre}

    9. Using SDSF, verify the device is online and ready.

       ```
       /D U,DASD,ONLINE
       ```
       {: pre}

4. If your z/OS instance is not created by using the standard z/OS stock image, run the appropriate TSO command in the z/OS instance to add the volume ID of the newly formatted volume to the list of target volumes for SDUMP. For example, SDUMP1 is the volume ID of the newly formatted volume.

   ```
   DD ADD,VOL=(SDUMP1)
   ```
   {: pre}

   You can skip this step if your z/OS instance is created by using the standard z/OS stock image because SDUMP is preconfigured to look for volumes with volume IDs: `SDUMP1`, `SDUMP2`, `SDUMP3`.
   {: important}

   The `ADD` command does not persist the change. For this change to persist over future system IPLs, make the corresponding changes to the appropriate PARMLIB (for example, `SYS1.PARMLIB(COMMND00)`).
   {: note}
