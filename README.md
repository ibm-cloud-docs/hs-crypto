# Hyper Protect Crypto Services docs

This repository stores documentation source files for both Hyper Protect Crypto Services and UKO on-prem.

  - [Jenkins build for HPCS](https://wcp-docs-team-jenkins.swg-devops.com/job/build/job/cloud-docs/job/hs-crypto/)
  - Slack channel: `#docs-hs-crypto` 
  - To view the live documentation, check out the [IBM Cloud Docs](https://cloud.ibm.com/docs/hs-crypto).
  
## Contributing
If you see a bug, you can contribute to this repository by [raising an issue](https://github.ibm.com/cloud-docs/hs-crypto/issues/new), or creating a pull request.

## Editing docs
Make any changes in the `source` branch of this repository. Commits to source run a build, lint your content, and publish changes to the [IBM Cloud stage docs](https://test.cloud.ibm.com/docs/hs-crypto). 

Because some of source files are shared between these two services, the `source` branch of this repository stores documentation source files for both Hyper Protect Crypto Services and UKO on-prem, and serves as the upstream for both service docs. To make changes to Hyper Protect Crypto Services source files, make sure to only touch the following subfolders:
  - `on cloud`: This is the main folder that hosts the HPCS source files. You need to most of the HPCS source file changes here, but there are some exceptions for file names started with 'uko-'. 
  - `reuse-snippets`: This folder contains files shared between HPCS and UKO on-prem. Some of the file names started with `uko-` in the `reuse-snippets` don't have actual content. These files should be updated in the `reuse-snippets` folder. For example, to update `uko-archive-template.md`, you need to go to the `reuse-snippets` folder, and update `uko-archive-template-reuse.md` instead.
- `reuse-pages`: This is a placeholder for reused pages in future releases. For now, no files are included.
  
## Publishing
Changes you've made in the `source` branch will be built to the `draft` and `review` branches, and then appear in a pull request that is opened against the `publish` branch called `Next prod push`. **Do not merge changes directly to draft, review, or publish branches, as the automation will overwrite these changes with the next push.** 

For more info on the branches, see the detailed guidance at [HPCS documentation Travis build guideline](https://github.ibm.com/cloud-docs/hs-crypto/wiki/HPCS-documentation-Travis-build-guideline/).

## Tagging 
If you are working on documentation for a new feature, make sure to tag your changes with a feature tag and include the tag in the `feature-flags.json` file. This will keep the `Next prod push` pull request clean if it is necessary to merge the `Next prod push` pull request before the documentation relating to the new feature is ready. 
  
For more information about how tags can be used, see [HPCS documentation Travis build guideline](https://github.ibm.com/cloud-docs/hs-crypto/wiki/HPCS-documentation-Travis-build-guideline/).

## Repository contacts

For any questions to this repository, contact Tiffany Li (shwtli@cn.ibm.com), Di Xu (xudi@ibm.com), or June Liu (liuxjep@cn.ibm.com).
