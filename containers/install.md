# Installation of {{site.data.keyword.uko_short}}
{: #install}

This section contains an overview over the required chapters for installation and migration of {{site.data.keyword.uko_short}}.

{{site.data.keyword.uko_short}} provides [z/OSMF workflows]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO) for most of the installation and migration steps. If you are unfamiliar with workflows, refer to the [workflow introduction chapter](getting-started-workflows.md).

## Installation from scratch
{: #install-from-scratch}

The following steps are required, if you are installing {{site.data.keyword.uko_short}} from scratch. 

1. Verify the [Planning](install-planning.md) section lists to ensure that you have the required installation skills and authorizations.
1. Verify that all [Program requirements](install-requirements.md) are met and that you have the correct prerequisite software and hardware versions.
1. Perform the SMP/E installation. The [SMP/E overview chapter](install-smpe.md) lists the required FMIDs and components. However, the SMP/E installation itself is not part of this documentation. 
1. Reserve ports and potentially setup for AT-TLS as described in the [network configuration chapter](install-network-configuration.md).
1. Ensure you have all [required user IDs](install-user-ids.md) in place, both userids for installation and operation of {{site.data.keyword.uko_short}}. You can use a [workflow for the creation of the required user IDs and groups]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukousers/provision.xml). 
1. Create the required views and tables as described in the [database setup](install-database.md). You can use a [workflow for the creation of the database]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukodb/provision.xml)
1. Ensure you have all [certificates and keyrings](install-keyring.md) in place that are required by the {{site.data.keyword.uko_short}} liberty server. You can use a [workflow for the creation of the required certificates, keyrings and CA]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukokeyring/provision.xml)
1. Make sure that a [Liberty angel process](install-liberty-angel.md) is available before the {{site.data.keyword.uko_short}} liberty server can be started. 
1. Configure and start the [Liberty server](install-liberty-server.md) running the {{site.data.keyword.uko_short}} server component. You can use a [workflow for the configuration of the Liberty server]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukoserver/provision.xml)
1. Walk through the [Agent](install-agent.md) installation chapter, if you want to create keys for z/OS. You can use a [workflow for the agent setup]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukoagent/provision.xml)

The [uko_install.properties]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/properties) file should be used to define all required workflow variables. The workflows are described in more details as part of the individual installation chapters. 

## Migration of an existing installation
{: #install-migration-intro}

1. Verify that all [Program requirements](install-requirements.md) are met and that you have the correct prerequisite software and hardware versions.
1. Perform the SMP/E installation. The [SMP/E overview chapter](install-smpe.md) lists the required FMIDs and components. However, the SMP/E installation itself is not part of this documentation. 
1. Walk through the [migration chapter](install-migration.md) to migrate from an older version of {{site.data.keyword.uko_short}} or EKMF Web to the latest version.

{{site.data.keyword.uko_short}} provides z/OSMF workflows for migrating the [{{site.data.keyword.uko_short}} database]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukodb/updateDatabase.xml) and the [{{site.data.keyword.uko_short}} server]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/workflows/ukoserver/updateServer.xml). The [uko_migration.properties]({{site.data.keyword.uko_workflow_url}}/provisioning-workflows/UKO/properties) file should be used to define all required workflow variables. The workflows are descripbed in more detail as part of the [migration chapter](install-migration.md).


## Additional chapters
{: #install-additional-chapters}

* If you want to use {{site.data.keyword.uko_short}} in collaboration with EKMF Workstation, refer to the [EKMF Workstation installation](install-workstation.md) chapter that summarizes the additional steps and points to the required installation chapters to focus on. 
* The [Installation references](install-about-references.md) chapter contains references like configuration parameters or security profile descriptions

