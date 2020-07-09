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


# Activity Insights (beta)
{: #setup-activity}

With {{site.data.keyword.security-advisor_long}}, you can continuously monitor your {{site.data.keyword.at_short}} logs to identify unauthorized or suspicious behavior and changes in your resources. You can use rule packages that are based on best practices that are provided by the service or create your own custom rules.
{: shortdesc}

Built-in insights are available for Kubernetes clusters on classic infrastructure only.
{: important}


## Before you begin
{: #activity-prereq}

To get started with Activity Insights, be sure that you have the following prerequisites.

- If you are working on Windows 10, activate [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10){: external}.
- Install the yq CLI:
  * For [macOS and Windows 10](http://mikefarah.github.io/yq/){: external}.
  * For CentOS, Red Hat, and Ubuntu run the following commands to install version 1.15.
    ```
    wget https://github.com/mikefarah/yq/releases/download/1.15.0/yq_linux_amd64       
    mv yq_linux_amd64 yq   
    chmod +x yq    
    mv yq /usr/local/bin/     
    yq -V
    ```
    {: codeblock}     
- Updated cURL binary: For CentOS and Red Hat, you can update by running `yum update -y nss curl libcurl`.
- The [{{site.data.keyword.cloud_notm}} CLI and required plug-ins](/docs/cli/reference/ibmcloud?topic=cli-install-ibmcloud-cli)
- The [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external} v1.10.11 or higher
- The [Kubernetes Helm (package manager)](/docs/containers?topic=containers-helm) v2.9.0 or higher.
- A standard Kubernetes cluster version v1.10.11 or higher



## Enabling Activity Insights
{: #activity-enable}

You can connect an instance of Cloud Object Storage and enable Activity Insights by using the Security Advisor UI.

1. Navigate to the [Security dashboard](https://{DomainName}/security-advisor#/overview) in the console.
2. Go to the **Settings** tab.
3. Click **Add bucket**. A modal appears.
4. Choose whether to create a bucket or use a bucket that you already have.
  
  If you choose to create a bucket through Security Advisor, the naming convention `<bucketName><uuid>.<region>` is used. For example, `sa.telemetric.12ab45.us-south`. If you want to provide your own name, you can create a bucket in Cloud Object Storage and then connect it to Security Advisor by choosing the existing bucket option.
  
  Only one bucket can be used with Activity Insights at a time.
  {: tip}

5. Select an option for **Resource group** and **Cloud Object Storage instance**. If you selected to use your own bucket, be sure to specify the bucket that you want to use.
6. Choose **Activity Insights**.
7. Describe your what your bucket is used for.
8. Click **Add bucket**.
9. Go to the **Integrations > Built-in Insights** tab.
10. Enable analysis for **Activity Insights**. Don't forget to install the needed components to finish enabling the feature.



## Installing {{site.data.keyword.security-advisor_short}} components
{: #activity-install-components}

You can install an agent to collect audit flow logs from your {{site.data.keyword.cloud_notm}} account. The logs are stored in your Cloud Object Storage instance where you can enable Activity Insights to analyze your logs for suspicious behavior.
{: shortdesc}

1. Clone the [Activity Insights](https://github.com/ibm-cloud-security/security-advisor-activity-insights){: external} repository to your local system.

  ```
  git clone https://github.com/ibm-cloud-security/security-advisor-activity-insights.git
  ```
  {: codeblock}

2. Change into the `security-advisor-activity-insights` folder.
3. Change into the directory for the version of the chart that you're using. Current supported versions include `v2.0` and `v3.0`.       

4. Extract the `.tar` file by running the following command.

  ```
  tar -xvf security-advisor-activity-insights.tar
  ```
  {: codeblock}

5. Change into `security-advisor-activity-insights` folder.
6. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to finish logging in.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

  <table>
    <caption>Table 1. IBM Cloud Endpoints by region</caption>
    <tr>
      <th>Region</th>
      <th>Endpoint</th>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>eu-gb</code></td>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>us-south</code></td>
    </tr>
  </table>

7. Set the context for your cluster.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

8. Install Helm by using the [Kubernetes Service integration docs](/docs/containers?topic=containers-helm).

9. Run the following command to install the Insights. The command validates the naming convention of your bucket, creates Kubernetes secrets, updates the values with your cluster GUID, and deploys Activity Insights.

  ```
  ./activity-insight-install.sh <cos_region> <cos_api_key> <cos_bucket> <at_region> <at_service_api_key> <default_memory_request> <memory_limit>
  ```
  {: codeblock}

  If you encounter an error, try running `helm init --upgrade`.
  {: tip}

  <table>
    <caption>Table 2. Install command components explained</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>cos_region</code></td>
      <td>The region where your COS instance is deployed. Options include: <code>us-south</code> and <code>eu-gb</code>.</td>
    </tr>
    <tr>
      <td><code>cos_api_key</code></td>
      <td>The [API key](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) that you created to access your COS instance and bucket. The key must have the platform role `writer`.</td>
    </tr>
    <tr>
      <td><code>cos_bucket</code></td>
      <td>The name of the bucket that you created in Cloud Object Storage to use with Activity Insights.</td>
    </tr>
    <tr>
      <td><code>at_region</code></td>
      <td>The region of the <a href="/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-regions">{{site.data.keyword.at_short}} instance</a>. Example: <code>us-south</code>.</td>
    </tr>
    <tr>
      <td><code>at_service_api_key</code></td>
      <td>Is a {{site.data.keyword.at_short}} [service key](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-export#api) for your {{site.data.keyword.at_short}} instance.</td>
    </tr>
    <tr>
      <td><code>default_memory_request</code></td>
      <td>The default memory that is requested when the pod is created during installation. If not provided, the default is <code>256Mi</code>.</td>
    </tr>
    <tr>
      <td><code>memory_limit</code></td>
      <td>The maximum amount of memory that is provided to the pod by the cluster. If not provided, the default is <code>512Mi</code>.</td>
    </tr>
  </table>


## Adding rule packages to COS
{: #activity-adding-rules}

A rule package is a JSON file that contains a list of rules that you want to monitor. You can download rule packages or [create your own](/docs/security-advisor?topic=security-advisor-activity#activity-packages). The {{site.data.keyword.security-advisor_short}} engine validates that each rule follows the correct syntax.
{: shortdesc}

1. Clone the following repository to get several preset rule packages. A folder is created on your local system with the name `security-advisor-activity-insights`.

  ```
  https://github.com/ibm-cloud-security/security-advisor-activity-insights.git
  ```
  {: codeblock}

2. Locally, create a folder with the name `IBM.rules/activities`.

3. Copy the JSON files from `security-advisor-activity-insights/security-advisor-ata-rule-packages` to `IBM.rules/activities`.

4. Navigate to your {{site.data.keyword.cloud_notm}} dashboard and select the COS service instance that is associated with Activity Insights.

5. On the **Buckets** tab of the service dashboard, select the bucket that is associated with Activity Insights.

5. On the COS instance home page, click **Upload** and select **Folders**.

6. If prompted, click **Install Aspera Connect client**. If you do not see a prompt, you already have the client installed. If you needed to install the client, repeat step 5 when the installation is finished.

7. Select the *IBM.rules/activities* folder.

8. Click **Upload**.

Want to use your own packages? Use one of the JSON files as a guide and create rules that fit your organizations needs. After you create the file, add it to the *IBM.rules/activities* folder in your COS instance. For more information about the types of rules and formatting, check out [Understanding rule packages](/docs/security-advisor?topic=security-advisor-activity).
{: tip}


## Deleting the components
{: #activity-delete}

If you no longer need to use Activity Insights, you can delete the service components from your cluster.
{: shortdesc}

1. Delete the service components by using Helm. Be sure to use the `-tls` flag if you have TLS enabled.

  If you installed version 2 of the chart, use the following command to delete the components.

    ```
    helm del --purge activity-insights [--tls]
    ```
    {: codeblock}
  
  If you installed version 3 of the chart, use the following command to delete the components.

    ```
    helm uninstall activity-insights --namespace security-advisor-activity-insights
    ```
    {: codeblock}

2. To clean up your cluster, run the following command.

  ```
  kubectl delete ns security-advisor-activity-insights
  ```
  {: codeblock}


  
  
