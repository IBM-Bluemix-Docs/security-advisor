---

copyright:
  years: 2021
lastupdated: "2021-02-17"

keywords: available network insights finding types, Network Insights,

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
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}


# Available network insights finding types
{: #network-insights-finding-types}

Network Insights monitor and analyze your VPC flow logs and identify Virtual Server Instances that might be compromised or attempts to compromise your VSI.
{: shortdesc}



## Suspicious Outbound Traffic
{: #suspicious-outbound-traffic}

#### Outbound approaches to suspicious servers

| Finding Type     |  Description     |
|:-----------------|:-----------------|
| `xforce-anonym_server` | One of the services in your asset is approaching a server that appears to be concealing its identity behind anonymization services. This data is based on IBM threat intelligence. |
| `xforce-malware_server` | One of the services in your asset is approaching a suspicious server, suspected of distributing malware. |
| `xforce-bot_server` | One of the services in your asset is approaching a server suspected as a bot. |
| `xforce-miner_server` | One of the services in your asset is approaching a server suspected as mining cryptocurrency. |
| `xforce-server_suspected_ratio` | High % of approaches by a client to destinations with bad reputation. One of the clients in your asset is approaching network addresses considered suspicious suggesting that your asset may be compromised. |
| `xforce-server_response_multiple_ips` | Client approaches and communicate with multiple destinations with bad reputation. One of the clients in your asset is interacting with multiple external services considered suspicious. |
| `xforce-server_response` | One of the clients in your asset was observed interacting with a suspicious network destination (two-way communication observed). |
| `xforce-server_response_multiple_flows` | Client performs multiple interactions with network destinations that have bad reputation. One of the clients in your asset repeatedly interacting with a suspicious services. |
{: caption="Table 1. Finding Types that are referred in the Suspicious Outbound Traffic" caption-side="bottom"}

#### Abnormally large payloads exchanged with suspicious servers

| Finding Type     |  Description     |
|:-----------------|:-----------------|
| `xforce-data_extrusion_multi` | Total volume sent to server peers with bad reputation exceed a threshold. One of the clients in your asset was observed sending large amount of data to destinations considered suspicious. |
| `xforce-data_extrusion` | Total volume sent to a server peer with bad reputation exceed a threshold. One of the clients in your asset was observed sending large amounts of data to a suspicious destination. |
| `xforce-server_weaponized_total_multi` | Total volume downloaded from suspected network addresses exceed a threshold. One of the clients in your asset was observed receiving large amount of data from suspected external services, which is indicative of Malware Installation. |
| `xforce-server_weaponized_total` | Total volume sent from a suspected external network address exceed a threshold. One of the clients in your asset was observed receiving large amounts of data from a suspicious service which may represent Malware Installation. |
{: caption="Table 1. Finding Types that are referred in the Suspicious Outbound Traffic" caption-side="bottom"}


## Suspicious Inbound Traffic
{: #suspicious-inbound-traffic}

#### Reconnaissance by suspicious clients

| Finding Type     |  Description     |
|:-----------------|:-----------------|
| `xforce-client_multiple_flows` | A peer with bad reputation is excessively approaching one or more closed port of your asset. An unexpectedly high number of approaches. |
| `xforce-clients_multiple_ips` | Peers with bad reputation are excessively approaching one or more closed port of your asset. An unexpectedly high number of approaches. |
| `xforce-distributed_vulnerability_scan` | Excessive number of unique peers with bad reputation are approaching open ports of the asset and might be scanning for the asset vulnerabilities. |
| `xforce-reconnaissance_multi` | Peers with bad reputation are excessively approaching unique closed ports (scanning). Your asset may be under reconnaissance by suspicious clients. |
| `xforce-vulnerability_scan` | A peer with bad reputation is excessively approaching open ports and might be scanning for asset vulnerabilities. |
| `xforce-reconnaissance` | A peer with bad reputation is excessively approaching unique closed ports of your asset (scanning). Your asset may be under reconnaissance by a suspicious client. |
| `xforce-client_response` | Your asset was observed interacting with a suspicious client (two-way communication observed). |
{: caption="Table 2. Finding Types that are referred in the Suspicious Inbound Traffic" caption-side="bottom"}

#### Abnormally large payloads sent by suspicious clients

| Finding Type     |  Description     |
|:-----------------|:-----------------|
| `xforce-client_weaponized` | A peer with bad reputation sends a large payload to your asset. Your asset was observed receiving large amount of data from a suspicious client which may represent an attempt to exploit your service. |
| `xforce-client_weaponized_total` | A peer with bad reputation sends accumulated large amount of data to your asset. Your asset was observed receiving large amounts of data from a suspicious client which may represent an attempt to exploit your service. |
{: caption="Table 2. Finding Types that are referred in the Suspicious Inbound Traffic" caption-side="bottom"}
