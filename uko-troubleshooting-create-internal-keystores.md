---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-20"

keywords: troubleshoot, problems, known issues, can't create internal keystores

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I create internal keystores?
{: #troubleshoot-create-internal-keystores}
{: troubleshoot}

When you try to add more internal KMS keystores, an error occurs.
{: shortdesc}

You receive the following error message when you try to add more internal KMS keystores:
{: tsSymptoms}

- From UI:

    > Adding keystore failed. The service was not able to add keystore `<keystore_ID>`.

- From API:

    > The operation on the keystore has failed. 
For a single service instance, you can create a maximum of 50 internal KMS keystores. You have reached the limits.
{: tsCauses}

Empty and delete an existing keystore so that you can create a new one.
{: tsResolve}


