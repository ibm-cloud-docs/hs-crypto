---

copyright:
  years: 2020, 2026
lastupdated: "2026-07-01"

keywords: troubleshoot, problems, known issues, blocked PIN on EP11 smart card

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why am I receiving a blocked PIN on EP11 smart card error?
{: #troubleshoot-block-smart-card}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}
{: troubleshoot}
{: support}

You try to use an EP11 smart card for an operation that requires personal identification number (PIN) entry and get an error.
{: shortdesc}

You might receive an error message similar to the following one:
{: tsSymptoms}

![Blocked PIN on EP11 smart card](/images/blocked-pin.gif "Blocked PIN on EP11 smart card"){: caption="Blocked PIN on EP11 smart card" caption-side="bottom"}

If an incorrect PIN is entered on an EP11 smart card 3 times, the smart card becomes blocked and can't be used for operations that require PIN entry.
{: tsCauses}

Take the following steps to unblock the EP11 smart card:
{: tsResolve}

1. Start the Smart Card Utility Program.
2. Select **EP11 Smart Card** &gt; **Unblock EP11 smart card** from the pull-down menu.
3. When prompted, insert the certificate authority smart card for the smart card zone of the EP11 smart card in smart card reader 1 and click **OK**.
4. When prompted, enter the first certificate authority PIN on the smart card reader PIN pad.
5. When prompted, enter the second certificate authority PIN on the smart card reader PIN pad.
5. When prompted, insert the EP11 smart card to be unblocked in smart card reader 2 and click **OK**.
