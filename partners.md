---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

keywords: Centralized security, security management, alerts, security risk, insights, threat detection

subcollection: security-advisor

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:script: data-hd-video='script'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}


# NeuVector
{: #setup-neuvector}

With [NeuVector](https://neuvector.com/){: external}, you can detect network threats and violations to prevent attacks of your container-based applications. Through monitoring, you can prevent exploits and breakouts by detecting root privilege escalations, port scans, reverse shells, and suspicious file system activity in your containers and hosts.
{: shortdesc}

When you configure the business partner connection, a card is created in your dashboard that summarizes the findings that are flagged by NeuVector. The NeuVector security report introduces one key performance indicator (KPIs) and a chart that represents findings data as it is updated daily. The chart contains the:

* Security events: Daily details of findings that are related to network threats and violations in your containers and hosts.
* Security events count: The total amount of findings that are related to network threats and violations in your containers and hosts.



## Before you begin
{: #partner-before}

Before you start integrating business partners, be sure that you have the following prerequisites.

* Ensure that you have an account with the business partner that you want to integrate.
* Ensure that you have the required permissions to generate the integration URL for the business partner service.
* Ensure that you have IAM administrator access to {{site.data.keyword.security-advisor_short}}.


## Integration wizard
{: #neuvector-wizard}

As an administrator with the needed permissions in both the {{site.data.keyword.cloud_notm}} and business partner accounts, you can use the integration wizard to quickly get up and running with NeuVector. The wizard has four basic steps:

* Establish trust and associate your {{site.data.keyword.cloud_notm}} and business partner accounts
* Copy the required information such as credentials and URLs between the accounts
* Install the business partner's finding metadata into {{site.data.keyword.security-advisor_short}}
* Validate the pairing by posting a finding from the business partner into {{site.data.keyword.security-advisor_short}}



## Configuring NeuVector
{: #configure-neuvector}

1. In the {{site.data.keyword.security-advisor_short}} dashboard, navigate to **Integrations > Partner Integrations** and select **NeuVector** from the options provided.

2. Click **Yes, connect my account to {{site.data.keyword.security-advisor_short}}**.

  If you don't already have an account, click **No, help me create an account > Create an account**. Fill out your information and wait for the NeuVector sales team to contact you to get started.
  {: note}

3. Give your connection a name. Be sure that the name is unique to your account and that you use only alpha-numeric characters, space, or a hyphen.

4. Optional: If you don't already have a configuration URL, click **Generate registration URL** to go to the NeuVector documentation and learn how to create the URL. Be sure that you have the NeuVector token that comes with your license to gain access to the docs.

5. [Get a setup URL](https://docs.neuvector.com/integration/ibmsa){: external} from NeuVector.

6. In the {{site.data.keyword.security-advisor_short}} dashboard, paste the URL in the **Enter the NeuVector setup URL** box.

7. Click **Connect Partner > Next**.

8. Click **Set up partner connection > Next > Done**.


## Verifying the connection
{: #neuvector-verify}

1. In the {{site.data.keyword.security-advisor_short}} dashboard, check whether the NeuVector card displays as expected.

2. Log in to NeuVector and [verify the connection](https://docs.neuvector.com/integration/ibmsa){: external}.

