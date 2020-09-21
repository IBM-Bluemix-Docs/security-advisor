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



# Direct connections
{: #direct-connections}

With {{site.data.keyword.security-advisor_short}}, you can integrate your existing custom security tools, whether open source, custom developed, or third party services. You can create a direct connection from {{site.data.keyword.security-advisor_short}} to the other tool by adding the URL to your list of integrations. By creating the link, you can easily monitor all of the tools that you use.
{: shortdesc}


## Before you begin
{: #custom-before-gui}

Before you can add the integration, you must first have an account with the partner that you want to integrate.

{{site.data.keyword.security-advisor_short}} does not persist any credentials that are related to the partner service. Enterprise users must authenticate by using SAML to both {{site.data.keyword.cloud_notm}} and to the business partner.
{: note}

## Configuring the connection
{: #custom-configure-connection}

1. Log in to your security tool and get your unique URL.

2. Log in to {{site.data.keyword.cloud_notm}} by using the console.

3. Click **Custom Integrations > Direct Connection**. A screen displays.

  1. Give your solution a name. You can use only alpha-numeric characters, white spaces, and dashes (-) in the name.

  2. Enter the URL for the solution in one of the following formats: `http://www.<website>.<domain>` or `https://www.<website>.<domain>`.

  3. Upload an icon or image to represent the tool.

  4. Click **Connect** to complete the configuration. {{site.data.keyword.security-advisor_short}} creates the artifacts that are required for integration such as the service ID, API key, account ID, and metadata. The `writer` role is assigned.