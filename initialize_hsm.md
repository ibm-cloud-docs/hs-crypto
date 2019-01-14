---

copyright:
  years: 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Initializing crypto instances to protect key storage
{: #initialize-hsm}

Master keys protect the contents of key storage. Using the Trusted Key Entry plug-in, you can load the master key registers of crypto instances in your {{site.data.keyword.cloud}} user account with values that you choose and control.   
{:shortdesc}

The Trusted Key Entry plug-in provides a limited set of functions for managing domains on EP11 crypto modules assigned to an {{site.data.keyword.cloud_notm}} user account. The plug-in allows you to load your master key values. The master key value is not known to any part of the {{site.data.keyword.cloud_notm}} other than the target domains on the target crypto modules.

It might take 20-30 minutes for you to complete this task.

## Before you begin

Before you load master keys, install the latest Trusted Key Entry plug-in with the following command:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  **Tip**: To install the CLI plug-in, see [Setting up the CLI](/docs/services/hs-crypto/set-up-cli.html). When you log in to the [{{site.data.keyword.cloud_notm}} CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/cli/index.html#overview){: new_window}, you're notified when updates are available. Be sure to keep your CLI up-to-date so that you can use the commands and flags that are available for the Trusted Key Entry CLI plug-in.

You must also set the environment variable CLOUDTKEFILES on your workstation to indicate the subdirectory where key part files and signature key files are created and saved. The environment variable gives the absolute path of the subdirectory.

## Identifying the crypto module domains assigned to a user account
{: #IdentifyDomains}

Domains that are assigned to an {{site.data.keyword.cloud_notm}} user account are in groups known as *crypto instances*. You need to configure all domains in a crypto instance in the same way. If one part of the {{site.data.keyword.cloud_notm}} cannot be accessed, the domains in a crypto instance can be used interchangeably for load balancing or for availability.

Domains on an EP11 crypto module that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state known as *imprint mode*. The master key registers in all domains must be set the same. The same set of administrators must be installed in all domains, and all domains must exit imprint mode at the same time.

* To display the crypto instances and domains assigned to a user account, use the following command:
  ```
  ibmcloud tke domains
  ```
  {: pre}

  The SELECTED column in the output table identifies what domains will be targeted by subsequent administrative commands that are issued by the plug-in.

* To select additional domains, use the following command:
  ```
  ibmcloud tke domain-add
  ```
  {: pre}

  A list of the domains that are assigned to the current user account is displayed. When prompted, enter a list of domain numbers to be added to the selected list.

* To make domains unselected, use the following command:
  ```
  ibmcloud tke domain-rm
  ```
  {: pre}

  A list of domains that are assigned to the current user account is displayed. When prompted, enter a list of domain numbers to be removed from the selected list.

  In general, either all domains or none of the domains for a crypto instance should be selected. This causes subsequent administrative commands to update all domains of a crypto instance consistently. However, if the domains of a crypto instance become configured differently, you need to select and work with domains individually to restore a consistent configuration to all domains in a crypto instance.

* To compare the configuration settings of the set of selected domains, use the following command:
  ```
  ibmcloud tke domain-compare
  ```
  {: pre}

## Loading master keys

A crypto instance is implemented as one or more domains on IBM cryptographic coprocessors.

Before the new master key register can be loaded, install one or more administrators in the target domains and exit imprint mode.

To load the new master key register, complete the following tasks using the {{site.data.keyword.cloud_notm}} CLI plug-in:

1. **Generate one or more signature keys**

  A domain administrator must sign the command to load the new master key register. The first step is to generate a signature key on your workstation. The private part is used to create signatures. The public part is placed in a certificate that is installed in a target domain to define a domain administrator.

  **Important**: For added security, the signature key owner can be a different person from the master key part owners. The signature key owner should be the only person who knows the password associated with the signature key file.

  * To display the existing signature keys on the workstation, use the following command:
    ```
    ibmcloud tke sigkeys
    ```
    {: pre}

  * To generate and save a new signature key on the workstation, use the following command:
    ```
    ibmcloud tke sigkey-add
    ```
    {: pre}

    When prompted, enter an administrator name and a password to protect the file. You must remember the password. If the password is lost, the signature key cannot be used.

2.  **Load one or more domain administrators in the target domain**

  **Important**: To load a master key register, all key part files and the signature key file must be present on a common workstation. If the files were generated on separate workstations, you might need to rename the files before you transfer them to the common workstation to avoid a name collision. The key part file owners and the signature key file owner must be present together at the common workstation so they can enter the file passwords at the appropriate time when the master key register is loaded.

  After a domain leaves imprint mode, all administrative commands sent to the domain must be signed by an administrator that the domain recognizes.

  * To display the administrators that are installed in a domain, use the following command:
    ```
    ibmcloud tke domain-admins
    ```
    {: pre}

  * To install a new domain administrator, use the following command:
    ```
    ibmcloud tke domain-admin-add
    ```
    {: pre}

    A list of the signature key files that are found on the the workstation is displayed.

    When prompted, select the signature key file to be installed as a domain administrator. And then enter the password for the selected signature key file.

    You can repeat the command to create additional domain administrators, if needed. Any administrator can independently run commands in the domain.

  In imprint mode, the command to install a domain administrator does not need to be signed. After leaving imprint mode, domain administrators can still be added, but the command to install a domain administrator must be signed by a domain administrator that is already installed in the domain.

3. **Leave imprint mode in the target domain**

  A domain in imprint mode is not considered secure. You cannot run most of the administrative commands, such as loading the new master key register, in imprint mode.

  * After you install one or more domain administrators, exit imprint mode by using the command:

    ```
    ibmcloud tke domain-exit-impr
    ```
    {: pre}

    The command to exit imprint mode must be signed by one of the installed domain administrators.

  * To select the administrator to sign the command, use the command:

  **Tip**: The command to exit imprint mode must be signed by a domain administrator. After the domain leaves imprint mode, all commands to the domain must be signed.

    ```
    ibmcloud tke sigkey-sel
    ```
    {: pre}

    A list of signature key files found on the workstation is displayed.

    When prompted, enter the key number of the signature key file to select for signing subsequent administrative commands.

  If a signature key file is already selected for signing administrative commands, this is indicated when the list of signature key files is displayed.

4. **Generate a set of master key parts to use**

  Each master key part is saved in a password-protected file on the workstation.

  **Important**: You must generate at least two master key parts. For added security, three key parts can be used and each key part can be owned by a different person. The key part owner should be the only person who knows the password associated with the key part file.

  * To display the existing master key parts on the workstation, use the following command:
  ```
  ibmcloud tke mks
  ```
  {: pre}

  * To generate and save a random master key part on the workstation, use the command:
    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    When prompted, enter a description for the key part and a password to protect the file. You must remember the password. If the password is lost, you cannot use the key part.

  * To enter a known key part value and save it in a file on the workstation, use the following command:
    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    When prompted, enter the key part value as a hexadecimal string for the 32-byte key part.  And then enter a description for the key part and a password to protect the key part file.

5. **Load the new master key register**

  To load the new master key register, use the following command:
  ```
  ibmcloud tke domain-mk-load
  ```
  {: pre}

  A list of the master key parts that are found on the workstation is displayed.

  When prompted, enter the key parts to be loaded into the new master key register. And enter the password for each selected key part file.

6. **Commit the new master key register**

  Loading the new master key register places the new master key register in the full uncommitted state. Before you can use the new master key register to initialize or re-encipher key storage, place the new master key register in the full committed state.

  To commit the new master key register, use the following command:
  ```
  ibmcloud tke domain-mk-commit
  ```
  {: pre}

7. **Move the master key**

  Move the master key to the current master key register with the following command:

  ```
  ibmcloud tke domain-mk-setimm
  ```
  {: pre}

  When prompted, enter the password for the signature key file.

## Reference: Other Trusted Key Entry plug-in commands

The following list describes the remaining commands implemented by the plug-in and discusses when they would be used.

* **ibmcloud tke mk-rm**

  This command removes a file that contains an EP11 master key part from the workstation.

  After you enter the command, a list of EP11 master key parts that are found on the workstation is displayed. When prompted, enter the key number of the key part that is to be removed.

  After a key part is removed from the local workstation, it can no longer be used.

* **ibmcloud tke sigkey-rm**

  This command removes a file that contains a signature key from the workstation.

  After you enter the command, a list of signature keys found on the workstation is displayed. When prompted, enter the key number of the signature key file that is to be removed.

  Be cautious of removing a signature key from the workstation. If any domains that are assigned to the user account leave imprint mode, and if the signature key being removed from the workstation is the only installed administrator for the domain, executing new administrative functions in the domain is not possible after you remove the signature key. If no backup of the signature key file exists, the only way for recovery is to contact {{site.data.keyword.cloud_notm}} support to clear the domain and place it in imprint mode.

* **ibmcloud tke domain-admin-rm**

  This command removes an administrator from the selected domains.

  When this command is issued for a domain in imprint mode, this command does not need to be signed. After the domain leaves imprint mode, this command must be signed by an existing domain administrator.

  For a domain not in imprint mode, the command fails if the administrator being removed is the last administrator defined for the domain.


* **ibmcloud tke domain-zeroize**

  This command clears the selected domains and places them back in imprint mode.  All domain administrators are removed, and the new and current master key registers are cleared.

  When this command is issued for a domain in imprint mode, this command does not need to be signed. After the domain leaves imprint mode, this command must be signed by an existing domain administrator.

  When this command is issued to a group of domains, the current signature key must be recognized as a domain administrator by all domains not in imprint mode in order for the command to be accepted.


* **ibmcloud tke domain-mk**

  This command displays the status and verification pattern for the new and current master key registers for the selected domains.

* **ibmcloud tke domain-mk-clrcur**

  This command clears the current master key register in the selected domains.

  This command cannot be executed in imprint mode.

  Clearing the current master key register makes any key storage protected by the current master key unusable.

* **ibmcloud tke domain-mk-clrnew**

  This command clears the new master key register in the selected domains.

  This command cannot be executed in imprint mode.

* **ibmcloud tke domain-mk-setimm**

  This command moves the value of the new master key register to the current master key register, and clears the new master key register in the selected domains.

  This command cannot be executed in imprint mode.

  This command does not initialize or re-encipher key storage and should be used only when key storage in the target LPARs is prepared to accept the new master key value. If in doubt, do not use this command, because it can cause keys in an existing key storage to become unusable.

The following is a full list of plug-in commands. You can also find the commands by using the plug-in help function:
```
NAME:
   ibmcloud tke - A CLI plug-in to manage crypto module domains in the IBM Cloud
USAGE:
   ibmcloud tke command [arguments...] [command options]

COMMANDS:
   mks                Lists EP11 master key parts stored on this workstation.
   mk-add             Creates and saves a new EP11 master key part.
   mk-rm              Removes an EP11 master key part from this workstation.
   sigkeys            Lists the signature keys stored on this workstation.
   sigkey-add         Generates and saves a new signature key.
   sigkey-rm          Removes a signature key from this workstation.
   sigkey-sel         Selects the signature key to use to sign commands.
   domains            Displays the domains for the current resource group.
   domain-add         Adds domains to the set of domains to work with.
   domain-rm          Removes domains from the set of domains to work with.
   domain-admins      Lists administrators installed in the selected domains.
   domain-admin-add   Add a domain administrator to the selected domains.
   domain-admin-rm    Removes a domain administrator from the selected domains.
   domain-compare     Compares configuration settings of the selected domains.
   domain-exit-impr   Exits imprint mode in the selected domains.
   domain-zeroize     Zeroizes the selected domains.
   domain-mk          Displays master key registers for the selected domains.
   domain-mk-clrcur   Clears the current master key register.
   domain-mk-clrnew   Clears the new master key register.
   domain-mk-commit   Commits the new master key register.
   domain-mk-setimm   Does set immediate on the master key registers.
   domain-mk-load     Loads the new master key register.
   help, h            Show help
   ```
