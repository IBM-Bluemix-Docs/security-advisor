---

copyright:
  years: 2017, 2019
lastupdated: "2019-12-18"

keywords: centralized security, security management, alerts, security risk, insights, threat detection

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

# Config advisor findings
{: #config-advisor-findings}

With {{site.data.keyword.security-advisor_long}}, you can assess the configuration of your {{site.data.keyword.Bluemix_notm}} resources according to security and compliance best practices by running scans with Config advisor. You can view details about any issues that are found during the scan on the **Config advisor** page for {{site.data.keyword.security-advisor_short}}.

If you run a scan, and don't see any findings returned for your account, check to be sure that you have all of the [required access](/docs/services/security-advisor?topic=security-advisor-config-setup#config-permissions).
{: note}


## Edge protection findings
{: #config-protection}

When a scan is run, you might see results on the **Edge protection** card of the dashboard. Edge protection findings alert you to potential configuration problems concerning the security of connections between your browsers and your cloud services. 


| Finding           | Severity and Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `All CIS security features are turned off` | High severity: When the toggle is set to off, Cloud Internet Services (CIS) security is not activated. All Web Application Firewall (WAF) and DDoS protection are turned off. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, go to **Reliability > DNS** and enable the proxy for the relevant DNS records. |
| `Minimum TLS version is set to lower than 1.2` | High severity: You are running an older, unsecure version of the Transport Layer Security Protocol, which means that your private connections are more susceptible to being hacked. | To fix the issue, update your TLS version to at least 1.2 in your specific CIS instance and zone. |
| `Web Application Firewall is turned off` | High severity: Your WAF is tuned off, which means that nothing is monitoring the HTTP traffic between the web and your application, which leaves you more prone to susceptible to malicious attacks such as cross-sit scripting, SQL injections, and more. | To fix the issue, turn on WAF rules in your CIS instance. |
| `WAF rules do not conform with expected` | High severity: Your configuration does not follow the recommended WAF rules. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, enable the rule that is returned in the finding from the **Web Application Firewall** tab. |
| `Edge TLS is not secure` | Medium severity: Your Edge TLS state is either disabled or is in flexible mode, where connections to your origin are made by using plain text. This option is not recommended because the connection from the browser to your server is not secure. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, go to **Security > TLS**, and update **mode** to **End-to-end CA signed**. |
| `DNS security is not activated` | Low severity: DNS security protects your DNS record authenticity and prevents malicious actors from performing man-in-middle attacks. By turning this off, your sit victors can be routed to fraudulent servers. | To fix the issue, turn on DNS security by finding the specific CIS instance and zone. Then, activate DNS security from the **Reliability > DNS** tab. Be sure to add the generated DNS records to your registrar. |
{: caption="Table 1. Edge protection findings and their remediation steps" caption-side="top"}





## Data protection findings
{: #config-cos}

When a scan is run, you might see results on the **Data protection** card of the dashboard. These findings alert you to the potential misconfigurations that can lead to your private data being leaked. 

| Finding           | Severity and Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `COS bucket is not encrypted with BYOK` | High severity: You do not control your encryption keys. | To fix the issue, use {{site.data.keyword.keymanagementservicelong_notm}} to manage keys to protect your {{site.data.keyword.cos_full_notm}} bucket. |
| `COS bucket is not in a private network` | High severity: By not using a private network, you're missing an extra layer of protection. Sensitive data might travel through a public network. | To fix the issue, be sure that your bucket is configured with a list of authorized IPs if your data needs to remain private. |
| `COS bucket is publicly accessible via S3 canned ACLs` | High severity: By using the predefined rules of your S3 canned ACL, your data is publicly accessible. | To fix the issue, consider customizing your ACLs. |
| `COS object is publicly accessible via canned ACLs` | High severity: By using the predefined rules of your S3 canned ACL, your data is publicly accessible. | To fix the issue, consider customizing your ACLs. |
| `IAM policies allow public read access to a bucket` | High severity: Your IAM policies are too lax, which leaves your data publicly accessible. | To fix the issue, consider customizing your IAM policies. |
{: caption="Table 2. Data protection findings and their remediation steps" caption-side="top"}


## User access findings
{: #config-iam}

When the scan is run, you might see results on the **User access** card of the dashboard. These findings alert you to privileges to your resources potentially being over allocated. When assigning access, you should be sure that you assign your users only the access that they need. Follow the principle of least privilege by giving your users only as much access that is needed to complete the task. By following this principle, you are more prepared if one of your users becomes compromised.

| Finding           | Severity and Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `The number of account admins is higher the given threshold` | High severity: A user with administrative access is no longer meant to have it. | To fix the issue, revise your list of administrators and verify that only the users that need the access are included in the list. |
| `The number of 'All resources' managers is higher than the given threshold` | High severity: Your account IAM policies do not follow the `pricinciple of least privilege`. Users with access to all of your resources can perform create, retrieve, update, and delete operations and have control of your {{site.data.keyword.cloud_notm}} instances. |  To fix the issue, revise your list of administrators and verify that only the users that need the access are included in the list. |
| `The number of IAM admins is higher than the given threshold` | High severity: Your account IAM policies do not follow the `pricinciple of least privilege`. An IAM admin can grant access to other users that might not have a need for that access. | To fix the issue, revise your list of IAM admins and verify that only the users that need the access are included in the list. |
| `The number of {{site.data.keyword.keymanagementserviceshort}} managers is higher than the given threshold` | High severity: Your {{site.data.keyword.keymanagementserviceshort}} manager list does not follow the `pricinciple of least privilege`. Users with access to your {{site.data.keyword.keymanagementserviceshort}} instances can perform create, retrieve, update, and delete operations. A malicious user might delete a key, which would render the data that the key was protecting as inaccessible. | To fix the issue, revise your list of {{site.data.keyword.keymanagementserviceshort}} managers and verify that only the users that need the access are included in the list. |
| `Too many users are 'All resources' readers` | Medium severity: Your account IAM policies do not follow the `pricinciple of least privilege`. This finding can indicate data leakage as users that should not have read access might view the data. | To fix the issue, revise your list of `All resources` readers and verify that only the users that need the access are included in the list. |
| `User with role outside of access group` | Medium severity: Assigning users to access groups allows for immediate control of the user in the group. You can easily revoke or update privileges for several users at one time. By not using access groups for everyone, a user might go unnoticed and might compromise your data. | To fix the issue, revise your user permissions and verify that your users are part of the correct groups. For more information and best practices, see [{{site.data.keyword.cloud_notm}} IAM account setup](/docs/iam?topic=iam-account_setup).  |
| `The number of COS managers is above the given threshold` | Medium severity: Manager access to Cloud Object Storage instances should follow the `least privileged` principle. This means that users exist at a need-to-know information level. Users that are not managers should not be given manager access as they are then able to perform all operations that are granted to that role. | To fix the issue, revise the list of users that are assigned the manager role in COS and verify that only those that need that level of access, have it. |
{: caption="Table 3. IAM user access findings and their remediation steps" caption-side="top"}


