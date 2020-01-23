---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-23"

keywords: Configuration issues, centralized security, security management, alerts, security risk, insights, threat detection

subcollection: security-advisor

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Running Config advisor scans
{: #config-setup}

With {{site.data.keyword.security-advisor_long}}, you can gain visibility into security issues and vulnerabilities in your {{site.data.keyword.cloud_notm}} account. The config advisor feature of {{site.data.keyword.security-advisor_short}} runs scans that combine known security and compliance policies and best practices to identify potential issues in the configurations of resources in your account. By running the scans, evaluating the findings, and addressing any vulnerabilities that are found, you can ensure that you're being diligent in your security efforts.
{: shortdesc}


## Before you begin
{: #config-permissions}

If you are the account owner, you can run the config advisor scans as often as you'd like. However, if you want to delegate the capability to run these scans to another user in your account, you must give them specific access:

| Resource | Role |
|----------|------|
| {{site.data.keyword.security-advisor_short}} | Manager |
| Cloud {{site.data.keyword.cos_short}} | Reader, Viewer |
| {{site.data.keyword.cis_short}} | Reader, Viewer |
| IAM Identity Service account management service| Viewer |
| IAM Access Groups account management service | Viewer |
| User management account management service | Viewer |
| All IAM-enabled resources | Viewer |
{: caption="Table 1. Required access to run config advisor scans" caption-side="top"}

To make assigning this access easier, you can [create an access group](/docs/iam?topic=iam-groups#create_ag), which you assign the access that is described in the table only one time to the group. Then, you can add or remove users from the group as you need. To reduce the number of access assignments, you can assign the Viewer role on all account management services instead of the three separate assignments for the account management services.
{: tip}

If you want a user in your account to only view the findings of the scans, and not run the scans, assign them the Viewer role or higher on the {{site.data.keyword.security-advisor_short}} service.


## Running scans
{: #config-run}

The config advisor scans and provides findings only when you choose to run it, which means that you don't get new findings each time you log in. Instead, you can choose how often you want to run the scans and evaluate the latest findings for the configurations in your account. 

The scans run and find issues with {{site.data.keyword.cis_full_notm}}, {{site.data.keyword.cos_full_notm}}, and Identity and Access Management configurations in your account.
{: note}

When you run the config advisor scan, the findings are displayed on three separate cards on the config advisor page. For findings related to user access configuration issues, see the **User access** card. For network and workload protection issues, see the **Edge protection** card. And last, see the **Data protection** card for all data configuration issues. To start a scan, complete the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
1. From the **catalog**, search for **Security Advisor**, and select the tile.
1. Go to the Config advisor page.
1. Click **Start scanning**.

Scans can take a few minutes to complete depending on the number of resources that must be scanned in your account. The identified violations for your account don't include any personal or private data.
{: note}

For more information about the specific issues that might be found and how you can start addressing them, check out [Config advisor findings](/docs/services/security-advisor?topic=security-advisor-config-advisor-findings).
{: tip}
