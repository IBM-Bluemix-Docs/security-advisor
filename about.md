---

copyright:
  years: 2017, 2020
lastupdated: "2020-08-26"

keywords: Centralized security, security management, alerts, security alert, security risk, insights, threat detection

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


# About {{site.data.keyword.security-advisor_short}}
{: #about}

{{site.data.keyword.security-advisor_long}} enables centralized security management through a unified dashboard that provides alerts. The alerts notify security administrators to issues and guide them to understand, prioritize, manage, and resolve security issues that are related to their cloud applications and workloads.
{: shortdesc}

## Benefits of using the service
{: #about-benefits}

![The benefits of using {{site.data.keyword.security-advisor_short}} can be found further outlined in the surrounding text.](images/sa-benefits.png){: caption="Figure 1. {{site.data.keyword.security-advisor_short}} benefits" caption-side="bottom"}

<dl>
  <dt>Security risk and posture</dt>
    <dd>Application security remains important with constant news articles that announce a new data breach or hack. Security risks will always be a part of development and although attacks can be difficult to predict, one way to prevent them is by closely monitoring your cloud deployments. For example, the risks can be related to vulnerabilities in your container images that are in use, expiring certificates that can cause outage of your cloud service or application or suspicious clients or servers with a known bad reputation interacting with your clusters.</dd>
  <dt>Centralized security management</dt>
    <dd>You can see a consolidated view of all of your {{site.data.keyword.cloud_notm}} security services and integrated business partner services. You can select and subscribe to different services from the {{site.data.keyword.cloud_notm}} catalog.</dd>
  <dt>Threat detection</dt>
    <dd>{{site.data.keyword.security-advisor_short}} leverages the information that is gathered by IBM X-Force, other {{site.data.keyword.cloud_notm}} services, and business partner solutions to detect risks and threats before they become a security issue. The service also provides analytics in addition to vulnerability data and network activity data.</dd>
</dl>


## How it works
{: #how-it-works}

To make maintaining security at a large scale easy, {{site.data.keyword.security-advisor_short}} is designed as a micro-service on {{site.data.keyword.cloud_notm}}. The core micro-service that is provided is the findings API, which implements the mechanism for {{site.data.keyword.cloud_notm}} and business partner services to send security findings to your service dashboard.
{: shortdesc}

The service receives findings from:
* Pre-integrated {{site.data.keyword.cloud_notm}} services like Certificate Manager and Vulnerability Advisor
* Network Insights
* Activity Insights
* IBM business partners like NeuVector and Twistlock
* Custom integrations with your other security tools


![This image shows the way in which the components of {{site.data.keyword.security-advisor_short}} fit together. The service receives findings from varying sources such as Built in insights or custom tools and then displays them in the dashboard where your security advisor can see an overview of your security posture.](images/how-it-works.png){: caption="Figure 2. How the components of {{site.data.keyword.security-advisor_short}} fit together" caption-side="bottom"}


{{site.data.keyword.security-advisor_short}} is most helpful for security administrators. That role can take many names. The described roles might be performed by a single person or multiple people - depending on the size of your company. However, the offering was created to address the day-to-day requirements of a CISO or Security focal. Check out the following table for some example users:

<table>
  <caption>Table 1. Types of Security Administrators</caption>
  <tr>
    <th>Security role</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>CIO</td>
    <td>A CIO or an Enterprise architecture team defines security and compliance policies at a high level for the entire company.</td>
  </tr>
  <tr>
    <td>CISO</td>
    <td>A CISO decides how to implement the policies that are set by the CIO for the systems that are under their control. This could include middleware, servers, or architecture that is deployed. This person would define the security governance and security policies for the organization. They would monitor security risk and define controls to meet compliance standards such as ISO, or GDPR. This person also decides the tools that their teams use.</td>
  </tr>
  <tr>
    <td>Security focal</td>
    <td>This person supports the CISO and executes the needed security checks and investigates any potential risks or issues. </td>
  </tr>
</table>


## High-availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.security-advisor_short}} is a highly available, regional service that is supported in us-south and eu-gb regions. In each supported region, the service runs in several availability zones. The service supports manual cross-regional failover from `us-south` to `us-east` and from `eu-gb` to `eu-de`. 

In every region, a highly available Cloudant cluster contains three copies of the data. A daily backup of data to Cloud Object Storage is done and the backup is kept for 7 days.

If a regional disaster occurs, the available data is restored by {{site.data.keyword.security-advisor_short}} without any action from you.

