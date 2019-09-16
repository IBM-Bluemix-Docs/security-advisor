---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-16"

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
{: #inbound-network-findings}
IBM Cloud Config Advisor allows you to run as ad-hoc assessment of your account configuration. You will be able to
 view the configuration issues found under the **Config Advisor** section in the dashboard

## Edge Protection Findings

### All CIS security features are turned off
{: #cis-features-off}
<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>  
**Risk**

When toggle is off CIS security will not be activated. All WAF and DDoS protection is essentially turned off.

**Remediation Steps**
  
- Find the specific CIS instance and zone
- Go to Reliability > DNS
- Enable proxy toggle for relevant DNS records

### DNS Security is not activated
{: #dns-security-off}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>
  
**Risk**  

DNS security protects your DNS record authenticity and prevents malicious actors from performing man-in-the middle types of attacks. Turning this off may lead to your site victors being routed to fraudulent servers.

**Remediation Steps**

- Find your CIS instance and zone
- Go to Reliability > DNS
- Activate DNS Security and add the generated DS records to your registrar

### Edge TLS is not secure.
{: #tls-configuration}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>
  
**Risk**

Your Edge TLS state is either disabled or is in flexible mode, where connections to your origin will be made 
using plaintext. This option is not recommended the connection from the browser to your server are not secure.

**Remediation Steps** 

- Find your CIS instance and zone
- Go to Security > TLS
- Change mode to 'End-to-end CA signed'


### Minimum TLS version is set to lower than 1.2
{: #min-tls-version}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Running a older version of the transport layer security protocol is not secure. 
Your private connections might be hacked. Please ensure your TLS version is set to at least "1.2".

**Remediation Steps**

- Find your CIS instance and zone
- Apply minimum TLS version as 1.2 (at least)


### Web Application Firewall is turned off
{: #waf-off}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Turning off the Web Application Firewall, will stop monitoring the HTTP traffic between the web and your application. You may be more prone to malicious attacks such as cross-site scripting, SQL injections and etc.,

**Remediation Steps**

- Find your CIS instance and zone
- Turn on WAF rules

### WAF rules do not conform with expected
{: #waf-rules-dont-conform}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Not running with the same baseline of recommended Web Application Firewall rules.

**Remediation Steps**

- Find your CIS instance
- Go to "Web Application Firewall".
- Enable the specific rule that is mentioned in this finding.

### Missing or misconfigured deny-all rule
{: #deny-all-rule}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk** 

Increases chances of hacking into the system. Only ports mentioned directly should be allowed access. 

**Remediation Steps**

Add a 'catch-all' rule to deny access to all ports not mentioned specifically.


### Non-standard HTTP ports defined in Calico
{: #non-standard-http-ports}
<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk** 

Increases chances of hacking into the system. Only well-known ports such as 80, 443 should be allowed access.

**Remediation Steps**

Check that the non-standard port is indeed required by the cluster.

### Mismatch between Calico and CIS whitelists
{: #calico-cis-mismatch}
<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk**
 
Unsynchronised whitelists Increase the chance of hacking into the system. 

**Remediation Steps**

Update the calico whitelists to match the current CIS whitelists

## Cloud Object Storage (COS) Findings


### The number of COS managers is above the given threshold
{: #cos-number-of-managers-threshold}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Manager access to COS instances does not follow the "least privilege principle",
where access is limited to on a "need-to-know" basis.
Users that should not have managers access to the COS may perform manager role operations.

**Remediation Steps**

Revise the list of COS managers and verify only users that need the access are found in the list.

### COS bucket is not encrypted with BYOK
{: #cos-bucket-not-encrypted-with-byok}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk**

You do not control your encryption keys. 

**Remediation Steps**

Use IBM Cloud Key Protect managed keys to protect your COS bucket.

### COS bucket is not in a private network
{: #cos-bucket-not-in-private-network}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk** 

Missing additional layer of protection. Sensitive data might be traveling in public networks. 

**Remediation Steps**

If your data needs to be private make sure your bucket is configured with a list of authorized IPs.

### COS bucket is publicly accessible via S3 canned ACLs
{: #cos-bucket-publicly-accessible-s3-canned-acl}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk**

Your data is publicly accessible due to using the predefined rules of your S3 canned ACL.

**Remediation Steps**

Consider customizing your ACLs. 

### IAM policies allow public read access to a bucket
{: #cos-bucket-publicly-accessible-s3-canned-acl}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk**

Your data is publicly accessible due to lax IAM policy.

**Remediation Steps**

Consider customizing your IAM policies. 

### COS object is publicly accessible via canned ACLs
{: #cos-object-publicly-accessible-s3-canned-acl}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: High</span>

**Risk**

Your data is publicly accessible due to using the predefined rules of your S3 canned ACL.

**Remediation Steps**

Consider customizing your ACLs. 

## User Access Findings

### The number of account admins is above the given threshold
{: #iam-account-admins-above-threshold}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>
Note: look at IAM documentation and provide more examples, such as billing. What account admins can do.

**Risk**

Users that aren't meant to have access or users that should no longer have administrative access still have it.
May indicate an insider threat.

**Remediation Steps**

Revise the list of administrators and verify only users that need the access are found in the list.

### The number of 'All resources' managers is above the given threshold
{: #iam-all-resources-managers-threshold}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Account IAM policies does not follow the "Principle of least privilege". May indicate an insider threat.
Such users can perform CRUD operations and  have control over IBM cloud instances.

**Remediation Steps**

Review the list of administrators and verify only users that need the access are found in the list.

### Too many users are 'All resources' readers
{: #iam-too-many-all-resources-users-readers}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Account IAM policies does not follow the "Principle of least privilege".
May indicate data leakage, users that should not have read access may view the data. May indicate an insider threat.

**Remediation Steps**

Review the list of 'All resources' readers.

### The number of IAM admins is above the given threshold
{: #iam-admins-above-threshold}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Account IAM policies does not follow the "least privilege principle". 
Such users may grant further access to other users that should not have access. May indicate an insider threat.

**Remediation Steps**

Review the list of IAM administrators and verify only users that need the access are found in the list.

### The number of Key Protect managers is above the given threshold
{: #iam-key-protect-managers-above-threshold}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Key protect managers list does not follow the "Principle of least privilege". May indicate an insider threat.
Such users can perform CRUD operations and  have control over IBM Cloud Key Protect instances.
A malicious user may delete a key, rendering the data the key was protecting inaccessible.

**Remediation Steps**

Review the list of Key Protect managers and verify only users that need the access are found in the list.

### User with role outside of access group
{: #iam-user-with-role-outside-of-access-group}

<span style="color: darkorange;display: block;font-weight: bolder;">Severity: Medium</span>

**Risk**

Assigning users to access groups allows immediate control over the users in this group, such as revoking or updating
the privilege. A user outside of the group may slip control, and might indicate a compromised user with self assigned 
privileges.
For best practice refer to [IBM Cloud IAM account setup](https://cloud.ibm.com/docs/iam?topic=iam-account_setup){: external}. 
   
**Remediation Steps**

Review the user permission and ensure they are part of existing access group. Create new group if needed.