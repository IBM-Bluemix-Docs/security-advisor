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
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}




# Caveonix
{: #setup-caveonix}

Caveonix RiskForesight is a multi-tenant cyber and compliance risk management platform for hybrid cloud. The platform provides the ability to detect, predict, and act on potential issues by providing continuous automated monitoring and analysis of cloud workloads. If you work with Caveonix, you can create an integration between Cavenoix and {{site.data.keyword.security-advisor_short}}, to see the findings for all of your IBM Cloud resources in the {{site.data.keyword.security-advisor_short}} dashboard.
{: shortdesc}

## Understanding Caveonix findings
{: #understand-caveonix}

When you configure the connection, two cards are created in your dashboard that summarize the findings from Caveonix.

### Card 1: Compliance Posture Summary
{: #caveonix-compliance-summary}

The compliance posture summary card contains information about your infrastructure and application assets and how they relate to your compliance controls.

| Finding | Description |
|:--------|:------------|
| Total infrastructure assets | The total number of your infrastructure assets in the SDDC environment, which might include vCenter, NSX-V, NSX-T, ESXi, and more. |
| Total application assets | The total number of your application assets, which might include virtual machines. |
| Compliance controls passed | The total number of compliance controls that are deemed compliant to the compliance controls in your most recent evaluation. |
| Compliance controls failed | The total number of compliance controls that are deemed noncompliant in your most recent evaluation. |
{: caption="Table 1. Understanding the findings returned in the compliance posture summary" caption-side="top"}

### Card 2: Security Posture Summary
{: #caveonix-security-summary}

The security posture summary card contains information about security vulnerabilities, or cyber risks, that are pulled from an NVD data source. The findings are classified as critical, high, and new. 

| Finding | Description |
|:--------|:------------|
| Total CyberRisk findings | The total number of cyber risk findings that are found for your cloud services. |
| Critical CyberRisk findings | The number of cyber risks that were found with a critical severity. Be sure to address critical findings immediately to mitigate and reduce the impact that they can have on your environment. |
| High CyberRisk findings | The number of cyber risks that were found with a critical severity. Be sure to address these as quickly as possible to try to mitigate the impact. |
| New CyberRisk findings | The number of cyber risks that were found for your cloud services in your latest scan. Be sure to review these closely to ensure that you don't miss a potential risk. |
{: caption="Table 2. Understanding the findings returned in the security posture summary" caption-side="top"}

## Before you begin
{: #before-caveonix}

Before you get started, be sure that you have an account with Caveonix.
And that you have the required level of access to create the connection. To integrate Caveonix, you need the *Manager* role or higher for the {{site.data.keyword.security-advisor_short}} service.

Be sure that you also have the following {{site.data.keyword.cloud_notm}} information ready to provide:

* Customer ID
* Provider ID
* An API key

  If you don't already have an API key, you can create a new one. The key is used to gain access to all of the accounts that you apply policies to in RiskForesight. Be sure to assign the appropriate access.

* Region

  Region options include Dallas `us-south` and London `eu-gb`. 


## Creating the connection
{: #connect-caveonix}

To start viewing your Caveonix findings in the {{site.data.keyword.security-advisor_short}} dashboard, you must first create a direct connection and an asset library.

1. Optional: Create a [direct connection](/docs/security-advisor?topic=security-advisor-direct-connections) in the {{site.data.keyword.security-advisor_short}} UI by adding the `RiskForsight FQDN` as your URL.
2. In the Caveonix RiskForesight UI, go to **Admin > Admin Overview > CSP Management > Asset Repositories**.
3. Click the **Create Asset Repository** icon.
4. Select **{{site.data.keyword.security-advisor_short}}** as your **Type** of asset.
5. Select a location and cloud provider for your repository.
6. Provide the {{site.data.keyword.cloud_notm}} information that you obtained before you got started, including your **Customer ID**, **API key**, **Region**, and **Provider ID**.
7. Choose whether to enable the connection.
8. Click **Test connection** to verify that the connection is in place.
9. Click **Save**.


## Scheduling the job
{: #caveonix-job}

To start sending findings to security advisor, create and schedule a job.

1. In the RiskForesight UI, go to **Admin > Admin Overview > Organization Management > Schedule**.
2. Click the **Create job** icon.
3. Select **{{site.data.keyword.security-advisor_short}}** as your **Type** of asset.
4. Provide a name and select an organization.
5. Set the schedule on which you want to push findings to the **{{site.data.keyword.security-advisor_short}}** dashboard.
6. Select the asset repository that you previously created.
7. Choose whether to enable the job.
8. Click **Save**.

