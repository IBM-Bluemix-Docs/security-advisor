---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-27"

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


# Config Advisor Findings
{: #config-advisor-findings}

With {{site.data.keyword.security-advisor_long}}, you can assess the configuration of your IBM Cloud resources according to security and compliance best practices by running scans with Config Advisor. Any issues that are found during the scan can be viewed in the **Config Advisor** section of the dashboard.


## Edge Protection Findings
{: #config-protection}

When the scan is run, you might see results in the **Edge protection** card of the dashboard. Edge protection findings alert you to potential configuration problems concerning the security of connections between your browsers and your cloud services. 


| Finding           | Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `All CIS security features are turned off` | When the toggle is set to off, CIS security is not activated. All WAF and DDoS protection are turned off. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, go to **Reliability > DNS** and enable the proxy for the relevant DNS records. |
| `DNS security is not activated` | DNS security protects your DNS record authenticity and prevents malicious actors from performing man-in-middle attacks. By turning this off, your sit victors can be routed to fraudulent servers. | To fix the issue, turn on DNS security by finding the specific CIS instance and zone. Then, activate DNS security in the **Reliability > DNS** tab. Be sure to add the generated DNS records to your registrar. |
| `Missing or misconfigured deny-all rule` | Without a properly configured `deny-all` rule, the chances of your system being hacked increase. You should ensure that the ports that are mentioned are the ones that are allowed access. | To fix the issue, add a `catch-all` rule to deny access to any ports that are not specifically mentioned. |
| `Non-standard HTTP ports defined in Calico` | Without properly defined HTTP ports, the chances of your system being hacked increase. | Check that any non-standard ports are actually required by your cluster. |
| `Mismatch between Calico and CIS whitelists` | Without properly synchronized whitelists, the chances of your system being hacked increase. | Update your calico whitelists to match your current CIS whitelists. |
{: class="simple-tab-table"}
{: caption="Table 1. High severity edge protection findings and their remediation steps" caption-side="top"}
{: #edge-protection-high}
{: tab-title="High severity"}
{: tab-group="edge-protection"}

| Finding           | Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `Edge TLS is not secure` | Your Edge TLS state is either disabled or is in flexible mode, where connections to your origin are made by using plaintext. This option is not recommended because the connection from the browser to your server is not secure. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, go to **Security > TLS** and update **mode** to **End-to-end CA signed**. |
| `Minimum TLS version is set to lower than 1.2` | You are running an older, unsecure version of the Transport Layer Security Protocol, which means that your private connections are more susceptible to being hacked. | To fix the issue, update your TLS version to at least `1.2` in your specific CIS instance and zone. |
| `Web Application Firewall is turned off` | Your WAF is tuned off, which means that nothing is monitoring the HTTP traffic between the web and your application, which leaves you more prone to susceptible to malicious attacks such as cross-sit scripting, SQL injections, and more. | To fix the issue, update turn on WAF rules in your CIS instance. |
| `WAF rules do not conform with expected` | Your configuration does not follow the recommended WAF rules. | To fix the issue, turn on CIS security by finding the specific CIS instance and zone. Then, enable the rule that is returned in the finding in the **Web Application Firewall** tab. |
{: class="simple-tab-table"}
{: caption="Table 2. Medium severity edge protection findings and their remediation steps" caption-side="top"}
{: #edge-protection-medium}
{: tab-title="Medium severity"}
{: tab-group="edge-protection"}



## Cloud Object Storage (COS) Findings
{: #config-cos}

When the scan is run, you might see results in the **Object Storage** card of the dashboard. COS findings alert you to the potential misconfigurations that can lead to the leakage of your private data.



| Finding           | Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `COS bucket is not encrypted with BYOK` | You do not control your encryption keys. | To fix the issue, use IBM Cloud Key Protect to manage keys to protect your COS bucket. |
| `COS bucket is not in a private network` | By not using a private network, you're missing an extra layer of protection. Sensitive data might travel through a public network. | To fix the issue, be sure that your bucket is configured with a list of authorized IPs if your data needs to remain private. |
| `COS bucket is publicly accessible via S3 canned ACLs` | By using the predefined rules of your S3 canned ACL, your data is publicly accessible. | To fix the issue, consider customizing your ACLs. |
| `IAM policies allow public read access to a bucket` | Your IAM policies are too lax, which leaves your data publicly accessible. | To fix the issue, consider customizing your IAM policies. |
| `COS object is publicly accessible via canned ACLs` | By using the predefined rules of your S3 canned ACL, your data is publicly accessible. | To fix the issue, consider customizing your ACLs. |
{: class="simple-tab-table"}
{: caption="Table 3. High severity COS findings and their remediation steps" caption-side="top"}
{: #cos-high}
{: tab-title="High severity"}
{: tab-group="cos"}

| Finding           | Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `The number of COS managers is above the given threshold` | Manager access to COS instances should follow the `least privileged` principle. This means that users exist at a need-to-know information level. Users that are not managers should not be given manager access as they are then able to perform all operations that are granted to that role. | To fix the issue, revise the list of users that are assigned the manager role in COS and verify that only those that need that level of access, have it. |
{: class="simple-tab-table"}
{: caption="Table 4. Medium severity COS findings and their remediation steps" caption-side="top"}
{: #cos-medium}
{: tab-title="Medium severity"}
{: tab-group="cos"}





## User Access Findings
{: #config-iam}

When the scan is run, you might see results in the **User access** card of the dashboard. These findings alert you to the potential over allocation of privileges to your resources. When assigning access, you should be sure that you assign your users only the access that they need. An easy way to keep track of this is the `principle of least privilege`. By giving your users the least access that they need to complete their tasks, you are more protected if one of your users becomes compromised.


| Finding           | Risk              | Remediation           |
|:------------------|:------------------|:----------------------|
| `The number of account admins is higher the given threshold` | A user might have administrative access that is no longer meant to have it. | To fix the issue, revise your list of administrators and verify that only the users that need the access are found in the list. |
| `The number of 'All resources' managers is higher than the given threshold` | Your account IAM policies do not follow the `pricinciple of least privilege`. Users with access to all of your resources can perform create, retrieve, update, and delete operations and have control of your IBM Cloud instances. |  To fix the issue, revise your list of administrators and verify that only the users that need the access are found in the list. |
| `Too many users are 'All resources' readers` | Your account IAM policies do not follow the `pricinciple of least privilege`. This finding can indicate data leakage as users that should not have read access might view the data. | To fix the issue, revise your list of `All resources` readers and verify that only the users that need the access are found in the list. |
| `The number of IAM admins is higher than the given threshold` | Your account IAM policies do not follow the `pricinciple of least privilege`. An IAM admin can grant access to other users that might not have a need for that access. | To fix the issue, revise your list of IAM admins and verify that only the users that need the access are found in the list. |
| `The number of Key Protect managers is higher than the given threshold` | Your Key Protect manager list does not follow the `pricinciple of least privilege`. Users with access to your Key Protect instances can perform create, retrieve, update, and delete operations. A malicious user might delete a key, which would render the data that the key was protecting in accessible. | To fix the issue, revise your list of Key Protect managers and verify that only the users that need the access are found in the list. |
| `User with role outside of access group` | Assigning users to access groups allows for immediate control of the user in the group. You can easily revoke or update privileges for several users at once. By not leveraging access groups for everyone, a user might go unnoticed and might compromise your data. | To fix the issue, revise your user permissions and verify that your users are part of the correct groups. For more information and best practices, see [IBM Cloud IAM account setup](/docs/iam?topic=iam-account_setup).  |
{: class="simple-tab-table"}
{: caption="Table 5. Medium severity IAM findings and their remediation steps" caption-side="top"}
{: #iam-medium}
{: tab-title="Medium severity"}
{: tab-group="iam"}


