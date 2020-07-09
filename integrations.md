---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-09"

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



# Integrations
{: #integrations}

With {{site.data.keyword.security-advisor_long}}, you can integrate other built-in insights, partner solutions, or create your own custom integrations.
{: shortdesc}


## Pre-integrated findings
{: #integrate-built-in}

With {{site.data.keyword.security-advisor_long}}, you can gain insight into potential issues through built-in service capabilities.
{: shortdesc}


Out of the box, {{site.data.keyword.security-advisor_short}} can integrate with:

* Certificate Manager for notifications that are related to certificate expiry and lifecycle.
* Vulnerability Advisor for details on image vulnerabilities and configuration issues.

To learn more, check out [Taking advantage of pre-integrated services](/docs/security-advisor?topic=security-advisor-setup-services)!

</br>

## Partner integrations
{: #integrate-partner}

Partner integrations are a way to enhance security for your {{site.data.keyword.cloud_notm}} deployments by creating a connection between {{site.data.keyword.security-advisor_short}} and other security tools that are working with IBM to ensure a seamless user experience.
{: shortdesc}

Current {{site.data.keyword.security-advisor_short}} partners include NeuVector and Twistlock.

Are you a partner and interested in integrating your solution with {{site.data.keyword.security-advisor_short}}? Reach out to our team by contacting Tim Branter at timmy@us.ibm.com.
{: tip}

### NeuVector
{: #integrate-neuvector}

[NeuVector](https://neuvector.com/){: external} provides a highly integrated, automated security platform for Kubernetes and Red Hat OpenShift that allows you to monitor and protect container network traffic. Specifically, East-West network traffic.

With NeuVector, you can detect network threats and violations to prevent attacks of your container-based applications. Through monitoring, you can prevent exploits and breakouts by detecting root privilege escalations, port scans, reverse shells, and suspicious file system activity in your containers and hosts.

For help with setting up your NeuVector instance, see [Partner solutions](/docs/security-advisor?topic=security-advisor-setup-partner#setup-neuvector).


### Twistlock
{: #integrate-twistlock}

[Twistlock](https://www.twistlock.com){: external} is uniquely able to prevent risk throughout the SDLC by preventing the deployment of vulnerable images across your environment. Automated and custom policy enforcement offers complete control at every stage of the application lifecycle. The Twistlock Intelligence Stream sources and aggregates vulnerability information directly from 30+ upstream projects, commercial sources, and proprietary research from Twistlock Labs.

With a focus on having the most precise data available to cover all of the layers of your stack, so you have accurate visibility and the lowest rate of false positives. Twistlock combines this data with knowledge of your actual deployments such as which containers are exposed to the internet, which run with high privilege, and which have other security mitigations in place, so you can always see what vulnerabilities are most critical in your specific environment.

For help with setting up your Twistlock instance, see [Partner solutions](/docs/security-advisor?topic=security-advisor-setup-partner#setup-twistlock).
</br>


## Custom integrations
{: #integrate-custom}

You might already have a security tool that you depend on. You can integrate that tool with the {{site.data.keyword.security-advisor_short}} dashboard so that all of your security information is centralized in one place!
{: shortdesc}

### Creating a direct connection
{: #create-direct-connect}

By using the {{site.data.keyword.security-advisor_short}} GUI, you can bookmark your internal and external security tools so that you have one point of access to everything from the {{site.data.keyword.security-advisor_short}} dashboard. For example, you could bookmark PagerDuty.

### Integrating your own tools with the API
{: #integrate-tools-api}

With the Findings API, you can integrate findings from your custom security tools into the {{site.data.keyword.security-advisor_short}} dashboard. This could be any custom or partner tool that generates a security alert or finding that also supports API-based interaction.

## Built-in Insights
{: #integrate-insights}

With built-in insights, you can detect potential issues by continuously monitoring your cluster and account logs. By monitoring network traffic and user activity, you can help ensure that your {{site.data.keyword.cloud_notm}} resources remain protected.
{: shortdesc}

### Network Insights (beta)
{: #integrate-network-insights}

With Network Insights (beta), you can monitor and analyze cluster network communication, both incoming and outgoing, between your Kubernetes cluster and external entities. By using integrated threat intelligence and anomaly detection, the service can identify reconnaissance attacks and potentially compromised assets. To learn more, check out [Network Insights](/docs/security-advisor?topic=security-advisor-network).

### Activity Insights (beta)
{: #integrate-activity-insights}

With Activity Insights (preview), you can continuously monitor your {{site.data.keyword.at_short}} logs to identify unauthorized or suspicious activity that is made by users or apps by using rule packages. You can use the rules packages that are provided by the service which are based on security best practices or you can customize the rules to fit your needs. To learn more, check out [Activity Insights](/docs/security-advisor?topic=security-advisor-activity).
