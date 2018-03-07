---

copyright:
  years: 2018
lastupdated: "2018-03-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Setting up IBM Cloud Security Advisor
{: #setup}
With IBM Cloud Security Advisor, you can use a variety of detection capabilities to find and alert you about suspicious network activity. To try out the Security Advisor network analysis feature, install the Security Advisor components in a Kubernetes cluster that is deployed to IBM Cloud Container Service. Then, you can see network insights and alerts in the Security Advisor dashboard.
{:shortdesc}

> **Note:** Security Advisor is a technology preview.


## Installing IBM Cloud Security Advisor
{: #install}
To enable the Security Advisor network analysis feature (experimental), deploy the IBM Cloud Security Advisor components to an IBM Cloud Container Service Kubernetes cluster. Net-flow data is collected for your cluster, and Security Advisor analyzes the Net-flow data to detect threats.  
{:shortdesc}

> **Note:** These components are deployed in the **monitoring** namespace in your cluster.

### Prerequisites
* Mac, Linux or Windows 10 developer workstation
  * Windows 10: [enable the Linux Subsystem feature](https://win10faq.com/install-run-ubuntu-bash-windows-10/)
* [Node.js](https://nodejs.org/en/) 6 or above
* [jQ](https://stedolan.github.io/jq/download/)
* [IBM Cloud Command Line Interface](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started) v0.6.5
* [IBM Cloud CLI Container Service plug-in](https://console.bluemix.net/docs/containers/cs_cli_install.html#cs_cli_install)
* [Kubernetes CLI (kubectl)](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [Kubernetes Helm (package manager)](https://docs.helm.sh/using_helm/#from-script)
* [A lite or paid Kubernetes cluster](https://console.bluemix.net/containers-kubernetes/catalog/cluster) in the **Dallas** region of IBM Cloud.



### Set up the Helm client
1. Log in to IBM Cloud.

  ```
  bx login -a https://api.ng.bluemix.net --sso
  ```
  {: pre}

2. List all of the clusters in the account to get the name of the cluster.

  ```
  bx cs clusters
  ```
  {: pre}

3. Target your CLI to the cluster.

  ```
  bx cs cluster-config <cluster-name-or-id>
  ```
  {: pre}

4. Set the path to the local Kubernetes configuration file as an environment variable. Example:

  ```
  export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
  ```
  {: pre}

5. Set up Helm in the cluster.

  ```
  helm init
  ```
  {: pre}

> **Note:** Keep this command-line window open and continue.

### Installing Security Advisor components

During the setup process, the following actions occur:
1. An IAM service ID and API key are generated in your IBM Cloud account so that your cluster can be identified by Security Advisor. If you have more than one cluster, run the installation for each cluster to generate service IDs and API keys for each cluster.
2. Cluster metadata is collected and used to complete the installation of worker node IP addresses, subnets, Ingress URL and IP address, cluster CRN, Log Analysis endpoint, space, and token.

To install the components:
1. Download and extract the [installation.zip](http://google.com) file.
2. From the same command-line window as the previous section, install the package.

  ```
  ./install.sh
  ```
  {: pre}

3. Verify that the components are installed properly by checking the Security Advisor dashboard. From the [IBM Cloud console](https://bluemix.net), click Security Advisor in the sidebar navigation.


## Uninstalling IBM Cloud Security Advisor
{: #uninstall}
### Removing Security Advisor components

Remove the Security Advisor components from your cluster and the service ID and API key from your IBM Cloud account.

1. Log in to IBM Cloud.

  ```
  bx login -a https://api.ng.bluemix.net --sso
  ```
  {: pre}

2. List all of the clusters in the account to get the name of the cluster.

  ```
  bx cs clusters
  ```
  {: pre}

3. Target your CLI to the cluster.

  ```
  bx cs cluster-config <cluster-name-or-id>
  ```
  {: pre}

4. Set the path to the local Kubernetes configuration file as an environment variable. Example:

  ```
  export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>/kube-config-prod-dal10-<cluster_name>.yml
  ```
  {: pre}

5. Run the uninstaller script.

  ```
  ./uninstall.sh
  ```
  {: pre}

6. Optional: Uninstall the Helm server component from the cluster.

  ```
  helm reset
  ```
  {: pre}
