{{site.data.keyword.uko_full}} provides efficient and security-rich centralized key management for IBM z/OS® data set encryption on IBM Z® (also referred to as Pervasive Encryption). It includes:

* A central repository. All keys are stored in a central repository with metadata such as activation dates and usage. By storing all key material in a central repository, backup can be easily achieved by including the database in existing database backup procedures. This facilitates easy recovery if keys are lost.
* Enhanced workflow. By employing automated, semi-automated, and bulk key management processes, workflow can be improved to enable your organization to effectively manage high key volumes.
* Policy based key generation. Keys are generated based on key templates that determine the attributes of keys, allowing keys to be consistently created on-demand. Supports the NIST key state model.
* Security-rich key generation. Key generation takes place within the IBM 4767 cryptographic coprocessor where keys are generated with a random number generator.
* Importing of existing keys. {{site.data.keyword.uko_short}} allows for importing and taking control of the management of existing Pervasive Encryption keys on z/OS systems.
* Role-based access control. The {{site.data.keyword.uko_short}} access control system is role-based and controls the access to functions. The security administrator can define functions that are available for each role and assign users to these roles.
* Dual control. {{site.data.keyword.uko_short}} roles can be configured to require that two or more persons must be involved to generate, activate, and distribute keys, thus providing dual control for critical operations.
* Audit logging. Every important activity is logged in an IBM Db2® table.
* A data set dashboard. This function provides an overview of data sets that are encryptable, already encrypted, or not encryptable. Various search options on this dashboard make it easy to get an overview of the encryption status of data sets on IBM Z.
* {{site.data.keyword.uko_short}} provides a user interface for centralized management of multiple z/OS systems simultaneously. Each z/OS system is managed by an installed {{site.data.keyword.uko_short}} agent instance, allowing for remote management of keys and z/OS data set encryption across the enterprise.

{{site.data.keyword.uko_short}} includes a pricing metric that enables flexibility in the way clients choose to implement production, test, and development environments. Pricing is determined by the number of simultaneous {{site.data.keyword.uko_short}} agent instances in use aggregated across an enterprise.
