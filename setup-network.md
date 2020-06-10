---

copyright:
  years: 2017, 2020
lastupdated: "2020-06-10"

keywords: Centralized security, security management, alerts, security risk, insights, threat detection

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


# Network Insights (beta)
{: #setup-network}

With {{site.data.keyword.security-advisor_long}}, you can collect and analyze your Kubernetes cluster network flow logs to detect any suspicious network activity by using learned patterns and threat intelligence. Network Insights is built with a community version of Skydive. 
{: shortdesc}


Built-in insights are available for Kubernetes clusters on classic infrastructure only.
{: important}


## Before you begin
{: #before-network}
Before you get started, be sure that you have the following prerequistes:

* A standard Kubernetes Service cluster version 1.14.10_1552 or higher.
* The [{{site.data.keyword.cloud_notm}} CLI and Kubernetes Service plug-in](/docs/cli?topic=cli-install-ibmcloud-cli)
* If you choose to install with Helm, you must also have the [Kubernetes Helm (package manager)](/docs/containers?topic=containers-helm) version 3 or higher


## Enabling Network Insights
{: #network-enable}

You can connect an instance of Cloud Object Storage and enable Network Insights by using the {{site.data.keyword.security-advisor_short}} UI.

1. Navigate to the [Security dashboard](https://{DomainName}/security-advisor#/overview) in the console.
2. Go to the **Settings** tab.
3. Click **Add bucket**. A modal appears.
4. Choose whether to create a bucket or use a bucket that you already have.
5. Select an option for **Resource group** and **Cloud Object Storage instance**. If you selected to use your own bucket, be sure to specify the bucket that you want to use.
6. Choose **Network Insights**.
7. Describe what your bucket is used for and click **Add bucket**.
8. Go to the **Integrations > Built-in Insights** tab.
9. Enable analysis for **Network Insights**.

## Obtaining service credentials
{: #cos-credentials}

After you've created your bucket, you can create a set of service credentials for your instance of Cloud Object Storage to use as part of your deployment.

1. In the Cloud Object Storage dashboard, click **Service Credentials**.
2. Click **New credential** and give your credential a name.
3. Assign the `Writer` IAM role.
4. Click **Add**.


## Installing {{site.data.keyword.security-advisor_short}} components
{: #network-install-components}

You can use Helm to install an agent that collects network flow logs from your Kubernetes cluster and store them in Cloud Object Storage. You can then enable Network Insights to analyze your logs and detect and alert you to suspicious network activity.
{: shortdesc}

Be sure to repeat the installation for each cluster that you want to monitor.
{: note}



To install the open source version of Skydive by using Helm, complete the following steps.

1. Clone the Skydive repository.

  ```
  git clone https://github.com/skydive-project/skydive-operator.git
  ```
  {: codeblock}

2. Locally, change in to the Skydive repository.

  ```
  cd skydive-operator/helm-charts/skydive/
  ```
  {: codeblock}

3. Log in to the {{site.data.keyword.cloud_notm}} CLI. Follow the prompts in the CLI to complete finish logging in.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

4. Set the context for your cluster.

    ```
    ibmcloud ks cluster config --cluster <cluster_name_or_ID>
    ```
    {: codeblock}

5. Optional: Create a namespace in your cluster. If you choose not to create a namespace, you can install the components into your default namespace.

  ```
  kubectl create ns insight
  ```
  {: codeblock}

6. Get your public subnet CIDR. If you don't currently have one, you can add a portable IP address. [Learn more](/docs/containers?topic=containers-subnets#adding_ips).

  ```
  ibmcloud ks cluster get --cluster <cluster_name> --show-resources
  ```
  {: codeblock}

7. To define your configuration, open the `values.yaml` file and use the following information as a guide to update the variables.

  ```
  exporter:
  enabled: true
  store:
  bucket: <bucket name>
  objectPrefix: "IBM/netflow/<bucket_region_name>/<cluster_id>/0"
  write:
  s3:
    endpoint: <endpoint>
    installLocalMinio: false
    region: <bucket_region_name>
    use_api_key: true
    api_key: <api_key>
  env_exporter:
    - name: SKYDIVE_PIPELINE_CLASSIFY_CLUSTER_NET_MASKS
        value: "10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 <public_subnet_CIDR>"
  ```
  {: screen}

  <table>
    <tr>
      <th>Parameter</th>
      <th>Value</th>
    </tr>
    <tr>
      <td><code>exporter.enabled</code></td>
      <td><code>true</code></td>
    </tr>
    <tr>
      <td><code>exporter.write.s3.endpoint</code></td>
      <td>The endpoint for your instance of Object Storage. For example: <code>https://s3.&lt;region&gt;.cloud-object-storage.&lt;app_domain&gt;.cloud</code></td>
    </tr>
    <tr>
      <td><code>exporter.write.s3.installLocalMinio</code></td>
      <td><code>false</code> </br>If this value is set to <code>true</code>, a default MinIO OS is installed locally into a container for testing purposes.</td>
    </tr>
    <tr>
      <td><code>exporter.write.s3.region</code></td>
      <td>The region where your instance of Cloud Object Storage is deployed. Options include: <code>us-south</code> and <code>eu-gb</code>.</td>
    </tr>
    <tr>
      <td><code>exporter.write.s3.use_api_key</code></td>
      <td><code>true</code></td>
    </tr>
    <tr>
      <td><code>exporter.write.s3.api_key</code></td>
      <td>The <code>api_key</code> that is found in the service credentials that you created in step 1.</td>
    </tr>
    <tr>
      <td><code>exporter.store.bucket</code></td>
      <td>The name of your bucket.</td>
    </tr>
    <tr>
      <td><code>exporter.store.objectPrefix</code></td>
      <td><code>IBM/netflow/&lt;bucket_region_name&gt;/&lt;cluster_id&gt;/0</code></td>
    </tr>
    <tr>
      <td><code>exporter.env_exporter.value</code></td>
      <td>The public subnet CIDR for your cluster.</td>
    </tr>
  </table>

8. Install the components. If you encounter an error, try running `helm init --upgrade`.

  ```
  helm install <release_name> -f values.yaml . --namespace insight
  ```
  {: codeblock}

  The release name is determined by you. It can be anything.
  {: tip}

You successfully configured your cluster to work with {{site.data.keyword.security-advisor_short}} Network Insights! Be sure to check the service dashboard regularly to quickly address any findings.



## Verifying the install
{: #network-check-logs}

To verify that everything is working correctly, you can check the logs and pod information for your Kubernetes cluster.

1. List all of the Skydive pods, including the agent and analyzer pods.

  ```
  kubectl get pods -n insight |grep 'skydive'
  ```
  {: codeblock}

2. Check the exporter logs to verify that objects are being sent to Cloud Object Storage.

  ```
  kubectl logs -f <skydive-analyzer-pod-name> -n insight skydive-exporter
  ```
  {: codeblock}



## Uninstalling Network Insights
{: #network-delete}

If you no longer have a need to use Network Insights, you can delete the service components from your cluster.
{: shortdesc}



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
  helm delete my-release -n insight
  ```
  {: codeblock}

4. Optional: If you created a namespace during installation, you can delete it.

  ```
  kubectl delete ns insight
  ```
  {: codeblock}

Be sure to delete the components for each cluster that you want to remove the agent from.
{: tip}


