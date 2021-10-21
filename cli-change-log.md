---

copyright:
  years:  2021
lastupdated: "2021-10-21"

keywords: change log for tke, updates to tke cli plugin, updates to cert manager cli plugin

subcollection: hs-crypto

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}


# {{site.data.keyword.hscrypto}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} command-line interface (CLI) plug-ins.
{: shortdesc}

## {{site.data.keyword.cloud_notm}} TKE CLI plug-in
{: #tke-cli-change-log}

### Version 1.2.3
{: #tke-cli-123}

Version 1.2.3 of the Trusted Key Entry (TKE) CLI was released on 30 June 2021.

Added the `ibmcloud tke failover-enable` command to enable or add failover crypto units after provisioning a {{site.data.keyword.hscrypto}} instance.

## {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} certificate manager CLI plug-in
{: #cert-manager-cli-change-log}

### Version 1.0.0
{: #cert-manager-cli-100}

Version 1.0.0 of the certificate manager CLI plug-in was released on July 2021.

This is the first release of the certificate manager CLI plug-in. You can use it to manage certificates and administrator signature keys for the second layer of authentication in GREP11 or PKCS #11 API connections.






## What functions or programs are pre-installed in the z/OS 2.4 stock image `ibm-zos-2.4-base-s390x`?
{: #faq-zos-vsi-1}
{: faq}

The following functions or programs are pre-installed in the z/OS stock image `ibm-zos-2.4-base-s390x`:

|Category  |Products Description  |
|--------------|------------------|
|**Base[^tabletext] z/OS, Exclusive[^tabletext2]** | * IBM z/OS Liberty Embedded \n * z/OS Container Extensions (zCX) \n * z/OS File System (was Distributed File Service) \n * Base Control Program (BCP) \n * Bulk Data Transfer (BDT) \n * Common Information Model (CIM) \n * Communications Server \n * Cryptographic Services \n * DFSMSdfp \n * ESCON Director Support \n * First Failure Support Technology/MVS (FFST/MVS) \n * Hardware Configuration Definition (HCD) \n * IBM HTTP Server powered by Apache \n * IBM Knowledge Center for z/OS \n * IBM z/OS Management Facility \n * Integrated Security Services \n * ISPF \n * JES2 \n * Language Environment® \n * Metal C Runtime Library \n * MICR/OCR \n * Network File System (NFS) \n * Runtime Library Extensions \n * SMP/E \n * Terminal Input Output Controller (TIOC) \n * Time Sharing Option/Extensions (TSO/E) \n * z/OS Font Collection \n * Time Sharing Option/Extensions (TSO/E) \n * z/OS Font Collection \n * z/OS OpenSSH \n * z/OS UNIX System Services |
|**Base z/OS, Non-Exclusive[^tabletext3]** | * 3270 PC File Transfer Program \n * Environmental Record Editing & Printing Program (EREP) \n * GDDM \n * High Level Assembler (HLASM) \n * ICKDSF (Device Support Facility) |
|**Optional[^tabletext4], Exclusive, not priced[^tabletext5]** |\n * Communications Server Security Level 3  \n * z/OS Security Level 3 |
|**Optional, Exclusive, Priced[^tabletext6]**  | * DFSMSdss \n * DFSMShsm \n * DFSMSrmm \n * DFSMStvs \n * DFSORT \n * Resource Measurement Facility (RMF)\n * Security Server (RACF) \n * System Display and Search Facility (SDSF) \n * XL Open C/C++ |
|**Optional, Non-Exclusive, Priced** | * GDDM-REXX  \n * High Level Assembler Toolkit (HLASM Toolkit) |
|**Middleware** | * CICS \n * DB2 \n * IRLM (DB2 Internal Resource Lock Manager) |
|**Programming Languages**| * Java comes with z/OS  \n * Cobol  \n * PL/1 \n * Python|
{: caption="Table 1. Content in the `ibm-zos-2.4-base-s390x` stock image" caption-side="bottom"}

Note:
  * [^tabletext]: The base elements deliver essential operating system functions.
  * [^tabletext2]: An element or feature is called exclusive to z/OS if it exists only within z/OS.
  * [^tabletext3]: An element or feature is called nonexclusive if it exists within both z/OS and as a separate product.
  * [^tabletext4]: The optional features are orderable with z/OS and provide additional operating system functions.
  * [^tabletext5]: Unpriced features are shipped to you only if you order them.
  * [^tabletext6]: Priced features are always shipped to you.

## What functions or programs are pre-installed and for development and test only?
{: #faq-zos-vsi-2}
{: faq}

The following additional functions are pre-installed in the z/OS stock image `ibm-zos-2.4-base-s390x-dev-and-test` on top of the stock image `ibm-zos-2.4-base-s390x`:

|Category  |Products Description  |
|--------------|------------------|
|**Development and test only**| * Nodejs \n * Go \n * Netview \n * System Automation \n * RSE (remote system explorer)  \n * RSE API \n * ZOAU: git, bash, cur, gzip, perl \n * IDz \n * ZUNIT \n * DBB \n * Debug \n * IBM Z Workload Scheduler - HCL |
{: caption="Table 2. Additional content in the `ibm-zos-2.4-base-s390x-dev-and-test` stock image" caption-side="bottom"}


## How can I interact with a z/OS virtual server instance?
{: #faq-zos-vsi-3}
{: faq}

You can access the z/OS virtual server instance by using the following supported methods:

   * Time Sharing Option/Extensions (TSO/E) and a limit set of TSO commands by using a TN3270 emulator
   * TSO/E and its menu-driven interface Interactive System Productivity Facility (ISPF) after logging on to the z/OS
   * z/OS Management Facility (z/OSMF) web browser interface and z/OS operator consoles
   * z/OS UNIX shell to write and invoke shell scripts and utilities, and use the shell programming language
