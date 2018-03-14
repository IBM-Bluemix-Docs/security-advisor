
1. Download and extract the [installation package](https://github.com/Bluemix-Docs/security-advisor/blob/staging/installation.tar.gz?raw=true).
2. From the same command-line window as the previous section, navigate to the extracted archive location and install the package.

  ```
  ./install.sh
  ```
  {: pre}

3. Verify that the components are installed properly by checking the Security Advisor dashboard. From the [IBM Cloud console](https://bluemix.net), click Security Advisor in the sidebar navigation.

## Removing Security Advisor components from a Kubernetes cluster
{: #cluster_uninstall}

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

5. Navigate to the extracted archive location and run the uninstaller script.

  ```
  ./uninstall.sh
  ```
  {: pre}

6. Optional: Uninstall the Helm server component from the cluster.

  ```
  helm reset
  ```
  {: pre}

</staging>
