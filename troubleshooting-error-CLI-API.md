---

copyright:
  years: 2020, 2023
lastupdated: "2023-07-05"

keywords: troubleshoot, problems, known issues, got a an error when I use CLI or API

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why am I receiving a `CKR_IBM_WK_NOT_INITIALIZED` error when I use CLI or API?
{: #troubleshoot-error-CLI-API}
{: troubleshoot}
{: support}

When you use CLI or API, you receive a `CKR_IBM_WK_NOT_INITIALIZED` error message.
{: shortdesc}

You might got an error message similar to the following message:
{: tsSymptoms}

> ibmcloud kp -i <service_instance_id> wrap <key_id>
> Wrapping key...
> FAILED
> Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259] GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]

When you ran the `ibmcloud tke cryptounit-compare` command, you didn't get a `Valid` confirmation on the CURRENT MASTER KEY REGISTER.
{: tsCauses}

Make sure that the HSM [master key](#x2908413){: term} is properly set.
{: tsResolve}
