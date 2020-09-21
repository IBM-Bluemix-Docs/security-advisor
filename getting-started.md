---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

keywords: getting started tutorial, getting started, security advisor, centralized security, security management, alerts, security risk, insights, threat detection, security advisor

subcollection: security-advisor

content-type: tutorial
account-plan: lite
completion-time: 10m

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

# Getting started with {{site.data.keyword.security-advisor_short}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With {{site.data.keyword.security-advisor_long}}, you can instantly view the security posture of your {{site.data.keyword.cloud_notm}} services through a single, centralized dashboard.
{:shortdesc}

{{site.data.keyword.security-advisor_short}} is enabled for all {{site.data.keyword.cloud_notm}} accounts in the Default resource group. As such, you do not need to provision any instance of the service.
{: tip}

The service receives security information from various sources and displays any security alerts or vulnerabilities that require your attention in the service dashboard. Out of the box, there are several pre-populated cards in your dashboard. These findings are from security services in {{site.data.keyword.cloud_notm}}, but you can also add cards or custom partner solutions so that all of your security tools can be accessed from the same location.

Through pre-integrated findings, you can monitor:

- Certificates that you manage with {{site.data.keyword.cloudcerts_long_notm}}
- Vulnerabilities in container images that are stored in {{site.data.keyword.registrylong_notm}}



## Get to the service dashboard
{: #start-dashboard}
{: step}

Ready to get started? You can get to the service dashboard by accessing the [{{site.data.keyword.compliance_long}}](/docs/security-compliance?topic=security-compliance-getting-started). 

1. In the {{site.data.keyword.cloud_notm}} console, click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) **> Security and Compliance**.
2. In the _Gain insight_ section of the navigation, click **Dashboard**.

    From the dashboard, you can view security information for the preconfigured integrated tools, such as Vulnerability Advisor and Certificate Manager. If your pre-integrated findings aren't displaying any information, you might not have any certificates or images for {{site.data.keyword.security-advisor_short}} to monitor. Learn more about what {{site.data.keyword.security-advisor_short}} needs to populate the dashboard cards in [Taking advantage of pre-integrated services](/docs/security-advisor?topic=security-advisor-setup-services).


## Next steps
{: #start-next}

Now that you've seen the dashboard in action, [learn more about {{site.data.keyword.security-advisor_short}}](/docs/security-advisor?topic=security-advisor-about) or start [integrating custom findings](/docs/security-advisor?topic=security-advisor-setup_custom).


## Availability
{: #start-availability}

Currently, you can take advantage of {{site.data.keyword.security-advisor_short}} in the Dallas (`us-south`) and London (`eu-gb`) regions.
