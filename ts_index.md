---

copyright:
  years: 2020
lastupdated: "2020-03-16"

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
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Troubleshooting
{: #troubleshooting}

If you have problems while you're working with {{site.data.keyword.security-advisor_long}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}


## Getting help and support
{: #getting-help-and-support}



You can find help by searching for information or by asking questions through a forum. You can also open a support ticket. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
{: shortdesc}

  * If you have technical questions about {{site.data.keyword.security-advisor_short}}, post your question on [Stack Overflow](https://stackoverflow.com/){: external}. Be sure to include the `security-advisor` and `ibm-cloud` tags.

  * For questions about the service and getting started instructions, use the [IBM Developer Answers](https://developer.ibm.com/){: external} forum. Be sure to include the `security-advisor` and `ibm-cloud` tags.


For more information about getting support, see [how do I get the support that I need](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## Error: namespaces "security-advisor-insights" is forbidden
{: #ts-error-helm-install}
{: troubleshoot} 
{: support}

{: tsSymptoms}
When you try to install Network or Activity Insights, you encounter the error:

```
namespaces “security-advisor-insights” is forbidden: User “system:serviceaccount:kube-system:default” cannot get resource “namespaces” in API group “” in the namespace “security-advisor-insights”
```
{: screen}

{: tsCauses}
The `kube-system` default service account does not have admin access in your cluster.

{: tsResolve}
Prior to installing one of the Built-in Insights offerings, you must install Helm. You can install Helm by using the [Kubernetes Service integration docs](/docs/containers?topic=containers-helm).


## Known issue: You can't create a custom solution occurrence
{: #ts-custom-occurrence}
{: troubleshoot} 
{: support}

{: tsSymptoms}
You try to create a custom solution occurrence but the information doesn't show in a browser and you receive no error message.

{: tsCauses}
Creating the occurrence failed because the name that you chose is in use.

{: tsResolve}
Choose another name for your occurrence.

## Known issue: Direct connection image doesn't update
{: #ts-known-cant-edit}

{: tsSymptoms}
When you upload or edit an image for a direct connection it doesn't immediately display.

{: tsCauses}
It is a known issue that images are not displaying correctly.

{: tsResolve}
To see the updated image, refresh your browser. The new image is displayed in the direct connection table.


## Known issue: Finding details from a notification payload direct link take 5 seconds to display in the dashboard
{: #ts-known-display-direct-link}

{: tsSymptoms}
When you try to access the findings details link found in the `issuer-url` of your notification payload, it takes 5 seconds to display in the service dashboard after the table is loaded.

{: tsCauses}
It is a known issue that there is a delay in displaying findings details when you access it from a direct link.
