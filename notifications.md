---

copyright:
  years: 2017, 2020
lastupdated: "2020-02-04"

keywords: Centralized security, security management, alerts, security risk, insights, threat detection, notifications, callback URL, compliance, standards, roles, notification channel, verify payload, public key

subcollection: security-advisor

---

{:external: target="_blank" .external}
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

# Configuring notifications
{: #notifications}

By configuring an {{site.data.keyword.security-advisor_long}} notification channel, you can be alerted to any reported vulnerabilities as soon as the report is available. With a fast alert time, you're able to immediately start an investigation into any reported issue and fix the vulnerability before it becomes a larger problem in your application. 
{: shortdesc}

With a process in place to handle alerts you can ensure that you're in compliance and prepared if or when an issue occurs. For example, some compliance standards require that issues must be responded to and closed within 24 hours, and the response is audited. With Security Advisor alerts in place, you are notified and can start resolving issues immediately.


## Before you begin
{: #notifications-before}

Before you get started with notifications, you must be assigned the proper IAM roles. Check out the following table to see which roles you need to interact with the service. For more information about roles, see [managing service access](/docs/security-advisor?topic=security-advisor-service-access).


## Configuring a notification method
{: #notification-method}

You can use a Callback URL to post notifications to the tools that you use. For example, you can send notifications to report to PagerDuty or automatically open an issue in GitHub.

**Important:** Your Callback URL endpoint must meet the following requirements:
* The endpoint must use the HTTPS protocol.
* The endpoint must not require HTTP headers. This requirement includes authorization headers.
* The endpoint must return a `200 OK` status code to indicate a successful notification delivery.



## Creating a notification channel
{: #channel-create}

To start receiving notifications immediately, you can configure a notification channel by using either the dashboard or the API.

### With the GUI
{: #channel-create-gui}

1. Navigate to the **Notifications channels** tab of the Security Advisor dashboard.
2. Click **Add notification channel**.
3. Using the following table as a guide, provide the following information.
  
 <table>
    <caption>Table 1. Configuring notifications with the GUI</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>Name</td>
      <td>The name of the channel.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Describe what the channel is used for. For example: <i>This channel sends high severity notifications as they happen.</i></td>
    </tr>
    <tr>
      <td>Type</td>
      <td>Current options include <code>Webhook</code>.</td>
    </tr>
    <tr>
      <td>Channel endpoint</td>
      <td>The location where you want to be notified. Examples include a slack channel, an email address, or a PagerDuty service.</td>
    </tr>
    <tr>
      <td>Severity</td>
      <td>The level of severity for the notification received. Options include: <code>low</code>, <code>medium</code>, and <code>high</code>. You must select at least one option when configuring your channel through the GUI.</td>
    </tr>
    <tr>
      <td>Alert source</td>
      <td>The source and type of finding that is received. Options include all alert source providers in your account and the set of finding types for each. You can select any or all of the sources and any or all of the finding types for a source. In addition to the custom alert source providers, six built-in providers are also available, which include Vulnerable images (VA), Network Insights (NA), Activity Insights (ATA), Certificate Manager (CERT), Config advisor (config-advisor) and All. Each built-in provider has their list of finding types.</td>
    </tr>
  </table>
  

4. Click **Save**. The channel is added to a list where you can track all of your channel configurations.

5. Test the connection by clicking the overflow menu in the row for the channel that you created. Select **Test the connection**. A test notification is sent to your endpoint. A test channel connection request triggers an alert as shown in the following example:

     ```
     {
        issuer : "Security Advisor Notification test",
        payload : {}
     }
     ``` 
     {: screen}
     
     Be sure to exclude alerts that are sent by the **Security Advisor Notification test** issuer from your final webhook implementation.
     {: note}

7. Optional: Update your configuration by clicking **Edit** in the overflow menu of the connection that you want to change.


### With the API
{: #channel-create-api}

1. Obtain an IAM bearer token by using the following steps. For more information, see the [IAM documentation](/docs/iam?topic=iam-getstarted).

  1. In the IBM Cloud dashboard, click **Manage > Access (IAM)**.
  2. Select **IBM Cloud API keys**.
  3. Click **Create an IBM Cloud API key**
  4. Give your key a name and describe it. Click **Create**. A screen opens with your key.
  5. Click **Copy** or **Download** your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
      --header "Content-Type: application/x-www-form-urlencoded" \
      --header "Accept: application/json" \
      --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
      --data-urlencode "apikey={apikey}" \
      "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

2. Run the following cURL command.

  ```
  curl -x POST "https://{region}.secadvisor.cloud.ibm.com/notifications/v1/{account_id}/notifications/channels"
  -H "accept: application/json"
  -H "Authorization: Bearer <IAM_Token>"
  -d {
    "name": "test-notification-channel",
    "description": "test-notification",
    "type": "Webhook",
    "endpoint": "<Endpoint>"
    "enabled": true
    "severity": ["low"]
    "alertSource": [
      {
        "provider_name": "ALL",
        "finding_types": ["ALL"]
      }
    ]
  }
  ```
  {: code}

  <table>
    <caption>Table 2. Configuring notifications with the API</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>Name</td>
      <td>The name of the channel.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Describe what the channel is used for. For example: <i>This channel sends high severity notifications as they happen.</i></td>
    </tr>
    <tr>
      <td>Type</td>
      <td>Current options include <code>Webhook</code>.</td>
    </tr>
    <tr>
      <td>Channel endpoint</td>
      <td>The location where you want to be notified. Examples include a valid callback URL.</td>
    </tr>
    <tr>
      <td>Severity</td>
      <td>The level of severity for the notification received. Options include: <code>low</code>, <code>medium</code>, and <code>high</code>. By default, <code>medium</code> and <code>high</code> are turned on.</td>
    </tr>
    <tr>
      <td>Provider</td>
      <td>The source and type of the finding that is received. <code>provider_name</code> is the ID of any provider in the account. If you're not sure which providers are available in your account, you can query the providers API: <code>/findings/v1/{accountId}/providers</code>. <code>finding_types</code> is the list of valid finding types for the provider name. If you're not sure which notes are available for each provider in your account, you can query the notes API: <code>/findings/v1/{account_id}/providers/{provider_id}/notes</code>. The <code>ALL</code> option can be specified for the <code>finding_types</code> which means that all notes for that provider are selected. There are 4 built-in providers in addition to custom alert source providers. For more information about the 4 providers and the supported finding types for each, review the following table.</td>
    </tr>
  </table>
  
<table>
    <caption>Table 3. Built-in providers and supported finding types</caption>
    <tr>
      <th>provider_name</th>
      <th>Supported finding types</th>
    </tr>
    <tr>
      <td>VA</td>
      <td><code>image_with_vulnerabilities</code>, <code>image_with_config_issues</code></td>
    </tr>
    <tr>
      <td>NA</td>
      <td><code>anonym_server</code>, <code>malware_server</code>, <code>bot_server</code>, <code>miner_server</code>, <code>server_suspected_ratio</code>, <code>server_response</code>, <code>data_extrusion</code>, <code>server_weaponized_total</code></td>
    </tr>
    <tr>
      <td>ATA</td>
      <td><code>appid</code>, <code>cos</code>, <code>iks</code>, <code>iam</code>, <code>kms</code>, <code>cert</code>, <code>account</code>, <code>app</code></td>
    </tr>
    <tr>
      <td>CERT</td>
      <td><code>expired_cert</code>, <code>expiring_1day_cert</code>, <code>expiring_10day_cert</code>, <code>expiring_30day_cert</code>, <code>expiring_60day_cert</code>, <code>expiring_90day_cert</code></td>
    </tr>
    <tr>
      <td>config-advisor</td>
      <td><code>appprotection-dns_not_proxied</code>, <code>appprotection-dnssec_off</code>, <code>appprotection-ssl_not_strict</code>, <code>appprotection-tls_min_version</code>, <code>appprotection-waf_off</code>, <code>appprotection-waf_rules</code>, <code>calico-deny_all_rule</code>, <code>calico-nonstandard_ports</code>, <code>calico-update_cis_whitelist</code>, <code>datacos-cos_managers</code>, <code>datacos-not_encrypted_via_kp</code>, <code>datacos-not_in_private_network</code>, <code>datacos-public_bucket_acl</code>, <code>datacos-public_bucket_iam</code>, <code>datacos-public_object_acl</code>, <code>iam-account_admins</code>, <code>iam-all_resource_managers</code>, <code>iam-all_resource_readers</code>, <code>iam-identity_admins</code>, <code>iam-kms_managers</code>, <code>iam-out_of_group</code></td>
  </tr>
    <tr>
      <td>ALL</td>
      <td><code>ALL</code></td>
    </tr>
   </table>
   
   `ALL` can be selected as the `provider_name`, which includes all providers and finding types. If `ALL` is specified as the `provider_name`, then a specific value can't be provided for `finding_types`. In this case, you can omit `finding_types` or specify `ALL`.
   {: tip}

  Example response:

  ```
  {
    "channel_id": "323fc870-78992-8ffa-97572ffe0205",
    "statusCode": 200
  }
  ```
  {: screen}

3. Test your connection.

  ```
  curl -X GET "https://{region}.secadvisor.cloud.ibm.com/notifications/v1/{ACCOUNT_ID}/test/notification/channel/{CHANNEL_ID}" -H "accept: application/json" -H "Authorization: {IAM_BEARER_TOKEN}"
  ```
  {: codeblock}

To edit your channel configuration, you can make an API call to the [`/update endpoint`](https://cloud.ibm.com/apidocs/security-advisor/notifications#update-a-channel){: external}.
{: tip}


## Verifying the payload
{: #verify}


When a notification is sent, you can use a public key to decrypt and verify the payload that is received. By using a public key, you can ensure that the information in the payload is not tampered with in any way.
{: shortdesc}

Example payload:

```
{
   "findings":[
      {
         "severity":"LOW",
         "issuer":"IBM Cloud Security Advisor",
         "issuer-url":"https://cloud.ibm.com/security-advisor#/findings?id=291266ca760e037c079edd4523242386/providers/test-provider/occurrences/ce90dc1-1-1-7",
         "id":"291266ca760e037c079edd4523242386/providers/test-provider/occurrences/ce90dc1-1-1-7",
         "payload-type":"findings",
         "payload-link":"https://us-south.secadvisor.cloud.ibm.com/findings",
         "provider":"cert-mgr",
         "payload":{
            "author":{
               "account_id":"291266ca760e037c079edd4523242386",
               "email":"user@test.com",
               "id":"IBMid-3100013FP0",
               "kind":"user"
            },
            "context":{
               "account_id":"291266ca760e037c079edd4523242386",
               "region":"US-South",
               "resource_crn":"cert-mgr",
               "service_crn":"cert-mgr-2"
            },
            "create_time":"2019-05-08T02:35:40.338757Z",
            "create_timestamp":1557282940339,
            "finding":{
               "certainty":"HIGH",
               "next_steps":[
                  {
                     "title":"Find your certificate."
                  },
                  {
                     "title":"Renew certificate with Certificate Authority."
                  },
                  {
                     "title":"Upload renewed certificate to Certificate Manager."
                  },
                  {
                     "title":"Redeploy certificate to SSL termination point."
                  },
                  {
                     "title":"Delete old certificate from Certificate Manager."
                  }
               ],
               "severity":"LOW"
            },
            "id":"ce90dc11-1",
            "insertion_timestamp":1557282940339,
            "kind":"FINDING",
            "long_description":"Certificate expiring in 90 days",
            "name":"291266ca760e037c079edd4523242386/providers/test-provider/occurrences/ce90dc1-1-1-7",
            "note_name":"29104aa4ec94471284be7d33bf1b1391/providers/security-advisor/notes/certmgr-expiring_90day_cert",
            "provider_id":"test-provider",
            "provider_name":"291266ca760e037c079edd4523242386/providers/test-provider",
            "reported_by":{
               "id":"certificate-manager",
               "title":"IBM Cloud Certificate Manager",
               "url":"https://cloud.ibm.com/docs/certificate-manager?topic=certificate-manager-gettingstarted#gettingstarted"
            },
            "short_description":"Certificate expiring in 90 days",
            "update_time":"2019-05-08T02:35:40.338792Z",
            "update_timestamp":1557282940339,
            "update_week_date":"2019-W19-3"
         }
      }
   ]
}
```
{: screen}

In the previous example, `payload-link` refers to the Security Advisor findings API endpoint where a user can get more information about the findings that they can use to take appropriate action.
{: note}

### Obtaining the public key with the GUI
{: #payload-gui}

You can obtain the payload by using the GUI.
{: shortdesc}

1. Navigate to the **Notifications channels** tab of the Security Advisor dashboard.
2. Click **Download key**.

### Obtaining the public key with the API
{: #payload-api}

You can obtain the payload by using the API.
{: shortdesc}

1. Obtain an IAM bearer token by using the following steps. For more information, see the [IAM documentation](/docs/iam?topic=iam-getstarted).

  1. In the IBM Cloud dashboard, click **Manage > Access (IAM)**.
  2. Select **IBM Cloud API keys**.
  3. Click **Create an IBM Cloud API key**
  4. Give your key a name and describe it. Click **Create**. A screen opens with your key.
  5. Click **Copy** or **Download** your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
      --header "Content-Type: application/x-www-form-urlencoded" \
      --header "Accept: application/json" \
      --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
      --data-urlencode "apikey={apikey}" \
      "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

2. Download the public key.

  ```
  curl -X GET "https://{region}.secadvisor.cloud.ibm.com/notifications/v1/{Account_ID}/download_public_key" -H "accept: application/json" -H "Authorization: {IAM-token}"
  ```
  {: codeblock}


### Decrypting your public key
{: #channel-decrypt}

Now that you have your public key, you can use [JWT](https://jwt.io/){: external} to decrypt and verify your payload. If you are working with Node.JS, your code snippet would look similar to the following.

```
const jwt = require("jsonwebtoken");
var decodedData = {}
try {
    decodedData = jwt.verify(<encrypted_payload_received>, <public_key>, { algorithms: ["RS256"] });
  } catch (err) {
    console.log(`JWT error : ${JSON.stringify(err)}`);
}
```
{: codeblock}


## Deleting a notification channel
{: #channel-delete}

You can delete a channel if you no longer need to monitor the information that is sent as notifications.

Want to take a break from receiving notifications but don't want to delete your configuration? No problem, disable your channel configuration instead. Then, when you're ready to use the configuration again, you can flip the switch to enabled and you're ready to go!
{: tip}


### With the GUI
{: #channel-delete-gui}

You can delete a single notification or bulk delete a group of notifications that you select.


1. Navigate to the **Notifications channels** tab of the Security Advisor dashboard.

2. Click the overflow menu in the row of the channel that you want to delete. Or, if you're deleting multiple channels at once, check the boxes for the channels that you would like to remove.

3. Select **Delete**.




### With the API
{: #channel-delete-api}

You can delete your channel configurations from the 

1. Obtain an IAM bearer token by using the following steps. For more information, see the [IAM documentation](/docs/iam?topic=iam-getstarted).

  1. In the IBM Cloud dashboard, click **Manage > Access (IAM)**.
  2. Select **IBM Cloud API keys**.
  3. Click **Create an IBM Cloud API key**
  4. Give your key a name and describe it. Click **Create**. A screen opens with your key.
  5. Click **Copy** or **Download** your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
      --header "Content-Type: application/x-www-form-urlencoded" \
      --header "Accept: application/json" \
      --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
      --data-urlencode "apikey={apikey}" \
      "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

2. Obtain your channel ID.

  ```
  curl -X GET "https://{region}.secadvisor.cloud.ibm.com/notifications/v1/{ACCOUNT_ID}/notifications/channels" -H "accept: application/json" -H "Authorization: {IAM_BEARER_TOKEN}"
  ```
  {: codeblock}

3. Delete the channel.

  ```
  curl -X DELETE "https://{region}.secadvisor.cloud.ibm.com/notifications/v1/{ACCOUNT_ID}/notifications/channels/{CHANNEL_ID}" -H "accept: application/json" -H "Authorization: {IAM_BEARER_TOKEN}"
  ```
  {: codeblock}


