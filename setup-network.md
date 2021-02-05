---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-05"

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


# Enabling Network Insights
{: #setup-network}

With {{site.data.keyword.security-advisor_long}}, you can continuously analyze your Virtual Private Cloud (VPC) network interface flow logs to detect any suspicious activity by using learned patterns and threat intelligence.
{: shortdesc}



## Before you begin
{: #before-network}

Before you get started with Network Insights, be sure that you have the following prerequisites.

* [An instance of VPC](https://{DomainName}/vpc-ext/provision/vpc)
* An IBM Cloud account with *editor* permissions for Security Advisor and VPC



## Connecting to Cloud Object Storage
{: #network-store-data}

Before you can analyze your network communication, Security Advisor must have access to your network flow logs that are stored in Cloud Object Storage. To create the connection between the services, you must store the logs in a Cloud Object Storage bucket and then grant the service access to the bucket.

You can choose to use an existing bucket that you already have created in Cloud Object Storage. Or, you can choose to create a bucket through the Security Advisor UI. When you choose to create a bucket through Security Advisor, the naming convention `BucketName_UUID.Region` is used. So, for example, your bucket name might be similar to `sa.telemetric.12ab45.us-south`. If you want to provide your own name, you can create a bucket through Cloud Object Storage by choosing the existing bucket option.

1. In the IBM Cloud console, navigate to [Security and compliance > Integrations > Data Settings](https://{DomainName}/security-advisor#/integrations).
2. Click **Connect bucket**.
3. Select whether to **Create a bucket** or to **Use an existing bucket**.

  If you selected create a bucket:

    1. Select a resource group and an instance of Cloud Object Storage.
    2. Select **Network Insights**.
    3. Optionally, provide a description.
    4. Click **Connect bucket**.

  If you create a new instance of Cloud Object Storage in addition to a new bucket, a service-to-service authorization policy between Security Advisor and Cloud Object Storage is created on your behalf. If you create a bucket within an instance of Cloud Object Storage that you already have provisioned, you must create a *reader* [service-to-service authorization policy](https://{DomainName}/iam/authorizations) between the two services before an analysis can be complete.   
  {: note}

  If you selected use an existing bucket:

    1. Select a resource group, an instance of Cloud Object Storage, and a bucket.
    2. Select **Network Insights**.
    3. Optionally, provide a description.
    4. Click **Connect bucket**.
    5. Create a *reader* [service-to-service authorization policy](https://{DomainName}/iam/authorizations) between Cloud Object Storage and Security Advisor.



## Collecting your flow logs
{: #collecting your flow logs}

Before it can be analyzed, you must collect your data. To do so, you can create a flow log that collects your network interface logs and funnels them into a Cloud Object Storage bucket.

You must have a service-to-service authorization policy between VPC and the same Cloud Object Storage bucket that you connected to Security Advisor in order to ensure that the data can be analyzed.
{: note}

1. In the IBM Cloud console, navigate to **VPC Infrastructure > Flow logs**.
2. Click **Create**.
3. Give your flow logs a name.
4. Select a resource group.
5. Optionally, add tags.
6. Select **Interface** for **Attach flow log connector to**.
7. Select your VPC, virtual server instance, and network interface.
8. Select the instance of Cloud Object Storage and the bucket that you connected to Security Advisor.
9. Click **Create flow log**.



## Enabling analysis
{: #enable-analysis-network}

Now that you've connected your Cloud Object Storage bucket and verified that your flow logs are being stored correctly, you can enable Network Insights to start analyzing them.


1. In the IBM Cloud console, navigate to [Security and compliance > Integrations > Built-in insights](https://{DomainName}/security-advisor#/integrations).
2. Toggle Activity Insights to **On**.

As results come in, you can see any flagged issues on the **Insights** or **Detailed findings** pages of the UI.


## Uninstalling Network Insights from your cluster
{: #network-delete}

After you've onboarded to the GA version of Network Insights, you can delete the beta service components from your cluster.

The Network Insights beta is deprecated as of **13 January 2021** and will no longer be supported as of **12 February 2021**. To remove the Network Insights components from your cluster, you can use the following steps.
{: deprecated}


### Uninstalling with Helm
{: #uninstall-network-helm}

To uninstall the components by using Helm, you must have used Helm to install them. To uninstall the components, you can use the following steps.



1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete finish logging in.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

2. Set the context for your cluster.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

3. Delete the components.

  ```
  helm delete my-release -n $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}

4. Delete the namespace.

  ```
  kubectl delete ns $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}

Be sure to delete the components for each cluster that you want to remove the agent from.
{: tip}



### Uninstalling with an operator
{: #uninstall-insights-operator}

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete finish logging in.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

2. Set the context for your cluster.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

3. Delete the custom resource to remove all Skydive related components.

  ```
  kubectl delete -f charts.helm.k8s.io_v1alpha1_netflowcollector_cr.yaml  -n $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}

4. Delete the operator and related resources.

  ```
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/operator.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/role_binding.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/role.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/service_account.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}

5. Optional: Remove the CRDs.

  ```
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/crds/charts.helm.k8s.io_netflowcollectors_crd.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  kubectl delete -f https://raw.githubusercontent.com/skydive-project/skydive-operator/master/deploy/crds/charts.helm.k8s.io_skydives_crd.yaml -n $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}

6. Delete the namespace.

  ```
  kubectl delete ns $SECURITY_INSIGHTS_NAMESPACE
  ```
  {: codeblock}


