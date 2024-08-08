# Hyper Protect Crypto Services docs

This repository stores documentation source files for both Hyper Protect Crypto Services and UKO on-prem.

  - [Jenkins build for HPCS](https://wcp-docs-team-jenkins.swg-devops.com/job/build/job/cloud-docs/job/hs-crypto/)
  - Slack channel: `#docs-hs-crypto` 
  - To view the live documentation, check out the [IBM Cloud Docs](https://cloud.ibm.com/docs/hs-crypto).
  
## Contributing
If you see a bug, you can contribute to this repository by [raising an issue](https://github.ibm.com/cloud-docs/hs-crypto), or creating a pull request.

## Editing docs
Make any changes in the `source` branch of this repository. Commits to source run a build, lint your content, and publish changes to the [IBM Cloud stage docs](https://test.cloud.ibm.com/docs/hs-crypto). 

As mentined, this repository stores documentation source files for both Hyper Protect Crypto Services and UKO on-prem. That is because of the UKO source files are shared between these two services. To make changes to Hyper Protect Crypto Services source files, make sure to only touch the following subfolders:
  - `on cloud`: This is the main folder that hosts the HPCS source files. You need to most of the HPCS source file changes here, but there are some exceptions for file names started with 'uko-'. 
  - `reuse-snippets`: This folder contains files shared between HPCS and UKO on-prem. Some of the file names started with `uko-` in the `reuse-snippets` don't have actual content. These files should be updated in the `reuse-snippets` folder. For example, to update `uko-archive-template.md`, you need to go to the `reuse-snippets` folder, and update `uko-archive-template-reuse.md` instead.
  
## Publishing
Changes will also appear in a pull request that is opened (or is already open) against the publish branch called `Next prod push`.
