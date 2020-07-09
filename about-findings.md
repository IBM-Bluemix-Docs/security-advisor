---
copyright:
  years: 2017, 2020
lastupdated: "2020-07-09"
keywords: Centralized security, security management, alerts, security alert, security risk, insights, threat detection
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


# The Findings API
{: #findings-api}

Based on [Grafeas](https://grafeas.io/){: external}, the Findings API is used to find and display occurences of security issues in your IBM Cloud account. The Findings API uses the artifact metadata API specification to store, query, and retrieve critical metadata. The findings are then summarized in cards in the Security Advisor dashboard that you can use to investigate any flagged issues.
{: shortdesc}


## Key concepts
{: #concepts}

Learn about different concepts that you might use while you work with {{site.data.keyword.security-advisor_short}}.
{: shortdesc}

<dl>
  <dt>Finding</dt>
    <dd>A finding is a priority security issue that is created when raw events are processed. Findings are made up of the key pieces of information that are needed to identify the who, what, when, and where of the issue. As a security admin, you can use {{site.data.keyword.security-advisor_short}} findings to prioritize and react to detected situations.</br> Findings are few and small in size but contain important insight that requires immediate attention. For example, your server is infected with malware or a certificate is about to expire.</dd>
  <dt>Key Performance Indicator (KPI)</dt>
    <dd>The Key Performance Indicator (KPI) is a measure that is used to indicate the risk of the findings to the security focal. KPIs provide an early signal of increasing risk exposures in various areas of enterprise cloud resources to the security focal. A KPI is triggered when a finding's value is out of bounds from the range of acceptable performance for specific security controls on services and workloads.</dd>
  <dt>Note</dt>
    <dd>A particular type of finding is defined as a note. Grafeas divides the metadata information into notes and occurrences. Notes are high-level descriptions of particular types of metadata. You can create different notes for each type of finding submitted by different providers.</dd>
    <dl>
      <dt>Occurrence</dt>
        <dd>An occurrence describes provider-specific details of a note. The occurrence contains the vulnerability details, remediation steps, and other general information.</dd>
      <dt>Card</dt>
        <dd>Metadata that is used to visualize the findings in the service dashboard is defined by note kind - <code>CARD</code>. {{site.data.keyword.security-advisor_short}} supports three types of KPI elements for a card: <ul><li>Numeric</li><li>Breakdown</li><li>Time series</li></ul></dd>
    </dl>
  <dt>Provider</dt>
    <dd>A provider is the tool or service that defines the type of finding (note) and then sends an occurrence of the finding to the service.</dd>
  <dt>Service CRN</dt>
    <dd>The Service CRN identifies the {{site.data.keyword.cloud_notm}} service that is involved in the finding. For instance, in a certificate expiry finding, the service instance ID, or CRN of the Certificate Manager service instance that reports the findings is included.</dd>
  <dt>Resource CRN</dt>
    <dd>The resource CRN identifies the specific resource that is involved in the finding. For example, when Network Analytics reports a finding, the Kubernetes cluster CRN is included to identify the cluster or resource affected.</dd>
</dl>


