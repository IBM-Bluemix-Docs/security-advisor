---

copyright:
  years: 2017, 2020
lastupdated: "2020-04-27"

keywords: Centralized security, security management, alerts, security risk, insights, threat detection, security advisor

subcollection: security-advisor

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
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


# Getting started tutorial
{: #getting-started}

With {{site.data.keyword.security-advisor_long}}, you can instantly view the security posture of your {{site.data.keyword.cloud_notm}} services through a single, centralized dashboard.
{:shortdesc}

{{site.data.keyword.security-advisor_short}} is enabled for all {{site.data.keyword.cloud_notm}} accounts in the Default resource group. As such, you do not need to provision any instance of the service.
{: tip}

The service receives security information from various sources and displays any security alerts or vulnerabilities that require your attention in the service dashboard. Out of the box, there are several pre-populated cards in your dashboard. These findings are from security services in {{site.data.keyword.cloud_notm}}, but you can also add cards or custom partner solutions so that all of your security tools can be accessed from the same location.

Through pre-integrated findings, you can monitor:

- Certificates that you manage with {{site.data.keyword.cloudcerts_long_notm}}
- Vulnerabilities in container images that are stored in {{site.data.keyword.registrylong_notm}}



## Getting to the service dashboard
{: #start-dashboard}

Ready to get started? You can get to the service dashboard in one of the following ways:

<ul>
  <li>By using the tile:
    <ol>
      <li>Log in to <a href="https://cloud.ibm.com/login" target="_blank">{{site.data.keyword.cloud_notm}}<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</li>
      <li>Navigate to the **Catalog** and click **Security and Identity**.</li>
      <li>Select the {{site.data.keyword.security-advisor_short}} tile. A dashboard opens where you can view security information for the preconfigured integrated tools such as Vulnerability Advisor and Certificate Manager.</li>
    </ol>
  </li>
  <li>By using the menu:
    <ol>
      <li>Log in to <a href="https://cloud.ibm.com/login" target="_blank">{{site.data.keyword.cloud_notm}}<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</li>
      <li>From your dashboard, click the Navigation menu to expand your options.</li>
      <li>Click **Security**. An overview of the security dashboard opens.</li>
      <li>Click **Getting Started** in the navigation to see general overview information about the service, or click **Dashboard** if you prefer to learn by seeing the service in action.</li>
    </ol>
  </li>
</ul>

Are your pre-integrated findings not displaying any information? You might not have any certificates or images for {{site.data.keyword.security-advisor_short}} to monitor. Learn more about what {{site.data.keyword.security-advisor_short}} needs to populate the dashboard cards in [Taking advantage of pre-integrated services](/docs/security-advisor?topic=security-advisor-setup-services).


## Next steps
{: #start-next}

Now that you've seen the dashboard in action, [learn more](/docs/security-advisor?topic=security-advisor-about) about how {{site.data.keyword.security-advisor_short}} can help you or start [integrating custom findings](/docs/security-advisor?topic=security-advisor-setup_custom).


## Availability
{: #start-availability}

Currently, you can take advantage of {{site.data.keyword.security-advisor_short}} in the Dallas (us-south) and London (eu-gb) regions.
