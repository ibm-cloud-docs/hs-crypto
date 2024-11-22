# Getting help and support

IBM Software Support provides assistance with product defects. Before contacting IBM Software Support, your company must have an active IBM software maintenance contract, and you must be authorized to submit problems to IBM.

It is recommended to collect MustGather data before contacting IBM Software Support. If you gather this documentation before you contact support it expedites the troubleshooting process, saves time, and will ensure that only one problem is reported on each case.

## Collecting MustGather data

Collecting MustGather data early, even before you open a case, helps IBM Support to quickly determine whether:

* Symptoms match known problems (rediscovery)
* There is a non-defect problem that can be identified and resolved
* There is a defect that identifies a work-around to reduce severity

### Collecting general information for {{site.data.keyword.uko_short}} problems

1. A complete description of the problem:
    * When did the problem first occur?
    * Has {{site.data.keyword.uko_short}} ever worked or is it a new setup?
    * Is the problem a one time failure or reoccurring?
    * Was software or hardware maintenance applied?
    * Did the failure occur while you did a specific task?
    * Is the failure that is occurring in more than one address space?
    * What was the intended outcome?
1. The {{site.data.keyword.uko_short}} version because the functions available in the product changes with the service level. The information can be found in the messages.log, for example: `Starting {{site.data.keyword.uko_short}} version 2.1.0.1 (back-end: 22.6.0-release.2.1.0.x.13, API: 2.2.4).` </br> You can also find this information when you log in to the {{site.data.keyword.uko_short}} user interface and navigate via the menu to **About**. 
1. The WebSphere Liberty server version, which is present in the {{site.data.keyword.uko_short}} server's job log, for example:</br>
`Launching ekmfweb (WAS FOR Z/OS 21.0.0.1/wlp-1.0.48.cl210120210113-1459) on IBM J9 VM, version 8.0.7.5 - pmz6480sr7fp5-20220208_01(SR7 FP5) (en_US)`</br>
and in the server's messages.log, for example:</br>
`product = WAS FOR Z/OS 21.0.0.1 (wlp-1.0.48.cl210120210113-1459)`
1. Operating system version, release, and maintenance levels
1. Version and release levels of related products (for example ICSF)

### Collecting (MustGather) data for {{site.data.keyword.uko_short}} problems

* {{site.data.keyword.uko_short}} server dump
* Any included xml configuration files not in the server's directory
* JCL that contains the environment variables
* {{site.data.keyword.uko_short}} server and Agent JES message log (SDSF started task log)

#### {{site.data.keyword.uko_short}} server dump

Contains: Zipped server file, which Contains trace.log, server.log, FFDCs, resources (for example *.aar, *.sar and *.ara files), server.xml. It will not contain included xml files and resources if they are not in the default locations
Collecting: /F <job_name>, DUMP
Location: Relative to the WLP_OUTPUT_DIR used by the server instance, default location of WLP_OUTPUT_DIR is `/var/IBM/ekmfweb/`. By default, the server output directory is: `/var/IBM/ekmfweb/<server_name>/<server_name>.dump-<date>_<time>.zip`
More information: [Set up trace and get a full dump for WebSphere Liberty](http://www.ibm.com/support/docview.wss?uid=swg21596714)


## Contacting IBM Software Support

Follow the steps in this topic to contact IBM Software Support:

1. Determine the business impact of your problem.
1. Describe your problem and gather background information.
1. Submit your problem to IBM Software Support using the [IBM Support Portal](https://www-947.ibm.com/account/userservices/jsp/login.jsp?persistPage=true&page=/support/entry/myportal/support).

Determine the business impact of your problem

When you report a problem to IBM, you will be asked to supply a severity level. Therefore, you need to understand and assess the business impact of the problem you are reporting. Use the following criteria:
* Severity
* Impact
* Characteristic

| Severity | Meaning | Description | 
| -- | -- | -- |
| 1 | Critical | You are unable to use the program, resulting in a critical impact on operations. This condition requires an immediate solution. |
| 2 | Significant | The program is usable but is severely limited. |
| 3 | Moderate | The program is usable with less significant features (not critical to operations) unavailable. |
| 4 | Minimal | The problem causes little impact on operations, or a reasonable circumvention to the problem has been implemented. |

Describe your problem and gather background information 

When explaining a problem to IBM, be as specific as possible. Include all relevant background information so that IBM Software Support specialists can help you solve the problem efficiently. To save time, know the answers to these questions:

What software versions were you running when the problem occurred?
Do you have logs, traces, and messages that are related to the problem symptoms? IBM Software Support is likely to ask for this information.
Can the problem be recreated? If so, what steps led to the failure?
Have any changes been made to the system? For example, hardware, operating system, networking software, and so on.
Are you currently using a workaround for this problem? If so, you might be asked to explain it when you report the problem.

To find out what information and files you will need to supply when opening a problem management record (PMR), see Collecting troubleshooting data for {{site.data.keyword.uko_short}} Enterprise Edition.
Submit your problem to IBM Software Support

You can submit your problem in one of two ways:

* Online: Go to the "Submit and track problems" page on the IBM Software Support site. Enter your information into the appropriate problem submission tool.
* By phone: For the phone number to call in your country, go to the contacts page of the IBM Software Support Handbook on the Web and click the name of your geographic region.

If the problem you submit is for a software defect or for missing or inaccurate documentation, IBM Software Support will create an Authorized Program Analysis Report (APAR). The APAR describes the problem in detail. Whenever possible, IBM Software Support will provide a workaround for you to implement until the APAR is resolved and a fix is delivered.

IBM publishes resolved APARs on the IBM product support Web pages daily, so that other users who experience the same problem can benefit from the same resolutions.
