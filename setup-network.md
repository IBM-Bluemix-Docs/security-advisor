---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-10"

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
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Enabling Network Insights
{: #setup-network}

With {{site.data.keyword.security-advisor_long}}, you can continuously analyze your Virtual Private Cloud (VPC) network interface flow logs to detect any suspicious activity by using learned patterns and threat intelligence.
{: shortdesc}



## Before you begin
{: #before-network}

Before you get started with Network Insights, be sure that you have the following prerequisites.

* [An instance of VPC](https://{DomainName}/vpc-ext/provision/vpc)
* An {{site.data.keyword.cloud_notm}} account with *editor* permissions for {{site.data.keyword.security-advisor_short_notm}} and VPC



## Connecting to Cloud Object Storage
{: #network-store-data}

Before you can analyze your network communication, {{site.data.keyword.security-advisor_short_notm}} must have access to your network flow logs that are stored in Cloud Object Storage. To create the connection between the services, you must store the logs in a Cloud Object Storage bucket and then grant the service access to the bucket. 

You can choose to use an existing bucket that you already have created in Cloud Object Storage. Or, you can choose to create a bucket through the {{site.data.keyword.security-advisor_short_notm}} UI. When you choose to create a bucket through {{site.data.keyword.security-advisor_short_notm}}, the naming convention `BucketName_UUID.Region` is used. So, for example, your bucket name might be similar to `sa.telemetric.12ab45.us-south`. If you want to provide your own name, you can create a bucket through Cloud Object Storage by choosing the existing bucket option.

1. In the {{site.data.keyword.cloud_notm}} console, navigate to [Security and compliance > Integrations > Data Settings](https://{DomainName}/security-advisor#/integrations).
2. Click **Connect bucket**.
3. Select whether to **Create a bucket** or to **Use an existing bucket**.

  If you selected create a bucket:

    1. Select a resource group and an instance of Cloud Object Storage.
    2. Select **Network Insights**.
    3. Optionally, provide a description.
    4. Click **Connect bucket**.

  If you create a new instance of Cloud Object Storage in addition to a new bucket, a service-to-service authorization policy between {{site.data.keyword.security-advisor_short_notm}} and Cloud Object Storage is created on your behalf. If you create a bucket within an instance of Cloud Object Storage that you already have provisioned, you must create a *reader* [service-to-service authorization policy](https://{DomainName}/iam/authorizations) between the two services before an analysis can be complete.   
  {: note}

  If you selected use an existing bucket:

    1. Select a resource group, an instance of Cloud Object Storage, and a bucket.
    2. Select **Network Insights**.
    3. Optionally, provide a description.
    4. Click **Connect bucket**.
    5. Create a *reader* [service-to-service authorization policy](https://{DomainName}/iam/authorizations) between Cloud Object Storage and {{site.data.keyword.security-advisor_short_notm}}.



## Collecting your flow logs
{: #collecting your flow logs}

Before it can be analyzed, you must collect your data. To do so, you can create a flow log that collects your network interface logs and funnels them into a Cloud Object Storage bucket.

You must have a service-to-service authorization policy between VPC and the same Cloud Object Storage bucket that you connected to {{site.data.keyword.security-advisor_short_notm}} in order to ensure that the data can be analyzed.
{: note}

1. In the {{site.data.keyword.cloud_notm}} console, navigate to **VPC Infrastructure > Flow logs**.
2. Click **Create**.
3. Give your flow logs a name.
4. Select a resource group.
5. Optionally, add tags.
6. Select **Interface** for **Attach flow log connector to**.
7. Select your VPC, virtual server instance, and network interface.
8. Select the instance of Cloud Object Storage and the bucket that you connected to {{site.data.keyword.security-advisor_short_notm}}.
9. Click **Create flow log**.



## Enabling analysis
{: #enable-analysis-network}

Now that you've connected your Cloud Object Storage bucket and verified that your flow logs are being stored correctly, you can enable Network Insights to start analyzing them.


1. In the {{site.data.keyword.cloud_notm}} console, navigate to [Security and compliance > Integrations > Built-in insights](https://{DomainName}/security-advisor#/integrations).
2. Toggle Activity Insights to **On**.

As results come in, you can see any flagged issues on the **Insights** or **Detailed findings** pages of the UI.


