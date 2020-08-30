---

copyright:
  years: 2017, 2020
lastupdated: "2020-08-30"

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



# Caveonix
{: #setup-caveonix}

Caveonix RiskForesight is a multi-tenant cyber and compliance risk management platform for hybrid cloud. The platform provides the ability to detect, predict, and act on potential issues by providing continuous automated monitoring and analysis of cloud workloads. By creating an integration between Cavenoix and {{site.data.keyword.security-advisor_short}}, you can manage the security of all of your {{site.data.keyword.cloud_notm}} services in the {{site.data.keyword.security-advisor_short}} even if you use Caveonix to monitor for risk.
{: shortdesc}

When you configure the connection, two cards are created in your dashboard that summarize the findings from Caveonix.

**Card 1: Compliance Posture Summary**

| Finding | Description |
|:--------|:------------|
| Total infrastructure assets | The total number of your infrastructure assets in the SDDC environment, which might include vCenter, NSX-V, NSX-T, ESXi, and more. |
| Total application assets | The total number of your application assets, which might include virtual machines. |
| Compliance controls passed | The total number of compliance controls that are deemed compliant to the compliance controls in your most recent evaluation. |
| Compliance controls failed | The total number of compliance controls that are deemed noncompliant in your most recent evaluation. |
{: caption="Table 1. Understanding the findings returned in the compliance posture summary" caption-side="top"}

**Card 2: Security Posture Summary**

| Finding | Description |
|:--------|:------------|
| Total CyberRisk findings | The total number of cyber risk findings that are found for your cloud services. |
| Critical CyberRisk findings | The number of cyber risks that were found with a critical severity. Be sure to address critical findings immediately to mitigate and reduce the impact that they can have on your environment. |
| High CyberRisk findings | The number of cyber risks that were found with a critical severity. Be sure to address these as quickly as possible to try to mitigate the impact. |
| New CyberRisk findings | The number of cyber risks that were found for your cloud services in your latest scan. Be sure to review these closely to ensure that you don't miss a potential risk. |
{: caption="Table 2. Understanding the findings returned in the security posture summary" caption-side="top"}

## Before you begin
{: #partner-before}

Before you start integrating business partners, be sure that you have an account with Caveonix.
And that you have the required level of access to create the connection. To integrate Caveonix, you need the *Manager* role or higher for the  {{site.data.keyword.security-advisor_short}}service.

Be sure that you also have the following information ready to provide:

* Caveonix customer ID
* Provider ID
* An API key
* Region


## Create the connection
{: #connect-caveonix}

To start viewing your Caveonix findings in the Security Advisor dashboard, create a direct connection and an asset library.

1. Create a [direct connection](/docs/security-advisor?topic=security-advisor-setup-custom-gui) in the {{site.data.keyword.security-advisor_short}} UI by adding the `RiskForsight FQDN` as your URL.

2. In the Caveonix RiskForesight UI, go to **Admin > Admin Overview > CSP Management > Asset Repositories**.

3. Click the **Create Asset Repository** icon.

4. Select **{{site.data.keyword.security-advisor_short}}** as your **Type** of asset.

5. Select a location and cloud provider for your repository.

6. Provide your {{site.data.keyword.cloud_notm}} **Customer ID**.

7. 

