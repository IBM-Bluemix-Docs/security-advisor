---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-05"

keywords: Configuration issues, centralized security, security management, alerts, security risk, insights, threat detection

subcollection: security-advisor

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Config Advisor (Preview)
{: #config-setup}

With {{site.data.keyword.security-advisor_long}}, you can easily perform an assessment of the current configuration of the resources in your 
{{site.data.keyword.cloud_notm}} account. The Config Advisor assessment combines known security and compliance policies and best practices to identify potential issues in your configuration. By running the scan and addressing any vulnerabilities that are found, you can ensure that you're being diligent in your security efforts.
{: shortdesc}

The configuration data that is scanned does not leave the local machine on which the assessment is run. The identified violations are sent to {{site.data.keyword.security-advisor_short}}, but do not include any personal or private data.
{: note}


## Before you begin
{: #config-before}

Before you can work with Config Advisor, you must have the following prerequisites.

- A stable version of the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).

- A stable version of [Docker](https://www.docker.com/products/docker-desktop){: external} installed locally.

- A service ID, with an [API key configured](/docs/iam?topic=iam-serviceidapikeys).


## Assigning the needed permissions
{: #config-permissions}

In order to run the Config Advisor scan, the service ID that is used must have the following permissions assigned. 

1. Open the {{site.data.keyword.cloud_notm}} dashboard.

2. Click **Manage > Access (IAM) > Users**.

3. You can either select a user from the provided list or add a user.

4. Click **Access Policies > Assign access > Assign access to resources**.

5. Using the following table as a guide, select a service and assign the associated permission level that is required.

  <table>
    <caption>Table 1. Required service ID permissions</caption>
    <tr>
      <th>Resource</th>
      <th>Role</th>
    </tr>
    <tr>
      <td>{{site.data.keyword.security-advisor_short}}</td>
      <td>Manager</td>
    </tr>
    <tr>
      <td>Cloud Object Storage (COS)</td>
      <td>Reader</td>
    </tr>
    <tr>
      <td>Cloud Internet Services (CIS)</td>
      <td>Reader</td>
    </tr>
    <tr>
      <td>Kubernetes Cluster</td>
      <td>Reader</td>
    </tr>
    <tr>
      <td>IAM Identity Service</td>
      <td>Viewer</td>
    </tr>
    <tr>
      <td>IAM Access Groups Service</td>
      <td>Viewer</td>
    </tr>
    <tr>
      <td>User Management</td>
      <td>Viewer</td>
    </tr>
    <tr>
      <td>Account Resources</td>
      <td>Viewer</td>
    </tr>
    <tr>
      <td>Optional: All Account Management Services</td>
      <td>Viewer</td>
    </tr>
  </table>


## Running the assessment
{: #config-run}

When you run the Config Advisor command, findings are created that are displayed in three separate cards in your {{site.data.keyword.security-advisor_short}} dashboard. Findings related to IAM configuration issues are found in the **User Access** card. Network and workload protection issues are found in the **Edge protection** card. And last, all COS configuration issues are found in the **Object Storage** card.

For more information about the specific issues that might be found and how you can begin remediation, check out [Config Advisor Findings](/docs/services/security-advisor?topic=security-advisor-config-advisor-findings).
{: tip}

1. Log in to {{site.data.keyword.cloud_notm}} by using the command prompt. Use the prompts to finish the log in process.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Set the region for the Container Registry.

  ```
  ibmcloud cr region-set global
  ```
  {: codeblock}

3. Log in to the Container Registry.

  ```
  ibmcloud cr login
  ```
  {: codeblock}

4. Run the Config Advisor scan.

  ```
  docker run icr.io/ibm/config-advisor:latest -k <APIKEY> <command> [options]
  ```
  {: codeblock}

  <table>
    <caption>Table 2. Config Advisor command options</caption>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>all</code></td>
      <td>Use the <code>all</code> command when you want to assess the entire configuration of your {{site.data.keyword.cloud_notm}} account.</td>
    </tr>
    <tr>
      <td><code>calico</code></td>
      <td>Use the <code>calico</code> command when you want to assess the IBM Cloud Kubernetes Service clusters in your account.</td>
    </tr>
    <tr>
      <td><code>cis</code></td>
      <td>Use the <code>cis</code> command to assess the configuration of the instances of IBM Cloud Internet Services that exist in your account.</td>
    </tr>
    <tr>
      <td><code>cos</code></td>
      <td>Use the <code>cos</code> command to assess the configuration of the instances of IBM Cloud Object Storage in your account.</td>
    </tr>
    <tr>
      <td><code>iam</code></td>
      <td>Use the <code>iam</code> command to assess the configuration of IBM Cloud Identity and Access Management in your account.</td>
    </tr>
  </table>

  To use specific versions of Config Advisor you can use tagging. To see your options, run `ibmcloud cr image-list --include-ibm --restrict ibm/config-advisor`.
  {: tip}

5. Go to your [{{site.data.keyword.security-advisor_short}} dashboard](https://cloud.ibm.com/security-advisor#/dashboard) in the `us-south` region and verify that you can see the created cards.

For more information about any issues that are returned, see [Config Advisor Findings](/docs/services/security-advisor?topic=security-advisor-config-advisor-findings).
{: note}
