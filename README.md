# Hyper Protect Crypto Services and UKO for IBM z/OS docs

This repository stores documentation source files for both Hyper Protect Crypto Services and UKO for IBM z/OS.

- [Jenkins build for HPCS](https://wcp-docs-team-jenkins.swg-devops.com/job/build/job/cloud-docs/job/hs-crypto/)
- Slack channel for HPCS: `#docs-hs-crypto` 
- Slack channel for UKO for IBM z/OS: `#docs-uko-for-zos`
- To view the live documentation, check out the [IBM Cloud Docs - HPCS](https://cloud.ibm.com/docs/hs-crypto) and [UKO for IBM z/OS Docs](https://www.ibm.com/docs/en/ukofz/3.1).
  
## Contributing

If you see a bug, you can contribute to this repository by [raising an issue](https://github.ibm.com/cloud-docs/hs-crypto/issues/new), or creating a pull request.

## Editing docs
Make any changes in the `source` branch of this repository. Commits to source run a build, lint your content, and publish changes to the [IBM Cloud stage docs](https://test.cloud.ibm.com/docs/hs-crypto) or [UKO for IBM z/OS stage docs](https://ibmdocs-test.dcs.ibm.com/docs/en/UKO_for_zOS_downstream_test). 

Because some of source files are shared between these two services, the `source` branch of this repository stores documentation source files for both Hyper Protect Crypto Services and UKO for IBM z/OS, and serves as the upstream for both service docs. 

### Editing Hyper Protect Crypto Services docs

To make changes to Hyper Protect Crypto Services source files, make sure to only touch the following subfolders:

- `oncloud`: This is the main folder that hosts the HPCS source files. You need to most of the HPCS source file changes here, but there are some exceptions for file names started with 'uko-'. 
- `reuse-snippets`: This folder contains files shared between HPCS and UKO for IBM z/OS. Some of the file names started with `uko-` in the `reuse-snippets` don't have actual content. These files should be updated in the `reuse-snippets` folder. For example, to update `uko-archive-template.md`, you need to go to the `reuse-snippets` folder, and update `uko-archive-template-reuse.md` instead.
- `reuse-pages`: This is a placeholder for reused pages in future releases. For now, no files are included.

### Editing UKO for IBM z/OS and Containers docs

To make changes to UKO for IBM z/OS or Containers source files, make sure to only touch the following subfolders:

- `zos`: This is the main folder that hosts the UKO for z/OS source files. You need most of the UKO for IBM z/OS source file changes here, but there are some exceptions for file names started with 'uko-'. 
- `containers`: This is the main folder that hosts the UKO for Containers files. 
- `reuse-snippets`: This folder contains files shared between HPCS and UKO for z/OS and UKO for Containers. Some of the file names started with `uko-` in the `reuse-snippets` don't have actual content. These files should be updated in the `reuse-snippets` folder. For example, to update `uko-archive-template.md`, you need to go to the `reuse-snippets` folder, and update `uko-archive-template-reuse.md` instead.
- `reuse-pages`: This is a placeholder for reused pages in future releases. For now, no files are included.

Variables:
- There is a central file for variable names called [cloudoekeyrefs.yml](https://github.ibm.com/cloud-doc-build/markdown/blob/master/cloudoekeyrefs.yml) that the cloud is using and that can be used. Here you find `uko_full_notm` which resolves to `Unified Key Orchestrator` for all platforms
- In addition, the local [keyref.yaml](https://github.ibm.com/cloud-docs/hs-crypto/blob/source/keyref.yaml) file is used to resolve additional variables for the `onprem` (`zos`) and `containers` folders. 
- Finally, the reuse-snippets contain [phrases.json](https://github.ibm.com/cloud-docs/hs-crypto/blob/source/reuse-snippets/phrases.json) which for example is used to resolve `uko_full` in the following way
  - `Unified Key Orchestrator`
  - ``
  - ``
  
## Publishing

### Hyper Protect Crypto Services

Changes you've made in the `source` branch will be built to the `draft` and `review` branches, and then appear in a pull request that is opened against the `publish` branch called `Next prod push`. 

**Note: Do not merge changes directly to draft, review, or publish branches, as the automation will overwrite these changes with the next push.**

For more infomation on the branches, see the detailed guidance at [HPCS documentation Travis build guideline](https://github.ibm.com/cloud-docs/hs-crypto/wiki/HPCS-documentation-Travis-build-guideline/).

### UKO for IBM z/OS

Changes you have made in the `source` branch will be built to the `release/3.1.0-copy` branch automatically. You can find the [GitHub repo](https://github.ibm.com/cccc/ekmf-web-docs/tree/release/3.1.0-copy) and the [WFM](https://wfm.dcs.ibm.com/product/UKO_for_zOS_downstream_test/637b0af746f3318cc78d7de09f4e7849). Then you can review the contents on the [staging site](https://ibmdocs-test.dcs.ibm.com/docs/en/UKO_for_zOS_downstream_test).

After you have reviewed the contents on the staging site, you can push the documentation to the production site through the [WFM](https://wfm.dcs.ibm.com/product/SSUAEQ_3.1/88ae68df00eba23ef8b7dd9b5a17fb62) by clicking the **Run**. 

Note that you also need to build the [installation PDF](https://wfm.dcs.ibm.com/product/SSUAEQ_3.1/583e92737381a7a4e447a6712e090912) and the [User PDF](https://wfm.dcs.ibm.com/product/SSUAEQ_3.1/a4680178e2637467760d7b2266669bfe).

### UKO for Containers

Changes you have made in the `source` branch will be built to the `release/containers` and `release/containers-copy` branch automatically. 
The [release/containers repo](https://github.ibm.com/cccc/ekmf-web-docs/tree/release/containers) is picked up by the [WFM SSTPB5_3.1 pipeline](https://wfm.dcs.ibm.com/product/SSTPB5_3.1) from where you can build to staging and production. 
In the future, we will setup a staging pipeline for the [release/containers-copy repo](https://github.ibm.com/cccc/ekmf-web-docs/tree/release/containers-copy).

Locations:
* `containers-draft` location builds only the containers directory and all others are removed. Pushes to https://github.ibm.com/cccc/ekmf-web-docs/tree/release/containers-copy
* `containers-publish` location builds only the containers directory and all others are removed. Pushes to https://github.ibm.com/cccc/ekmf-web-docs/tree/release/containers

Feature flags:
* There is now a feature flag called `containers` that can be used in the reuse-snippets to build to UKO for Containers only.
* The `onprem` feature flag will build to both, UKO for z/OS and UKO for Containers.
* The `zos` feature flag will build to UKO for z/OS exclusively

## Tagging 

If you are working on documentation for a new feature, make sure to tag your changes with a feature tag and include the tag in the `feature-flags.json` file. This will keep the `Next prod push` pull request clean if it is necessary to merge the `Next prod push` pull request before the documentation relating to the new feature is ready. 
  
For more information about how tags can be used, see [HPCS documentation Travis build guideline](https://github.ibm.com/cloud-docs/hs-crypto/wiki/HPCS-documentation-Travis-build-guideline/).

## Repository contacts

For any questions to this repository, contact Tiffany Li (shwtli@cn.ibm.com), Di Xu (xudi@ibm.com), or June Liu (liuxjep@cn.ibm.com).
