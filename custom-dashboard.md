---

copyright:
  years: 2018
lastupdated: "2018-3-14"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# What is a custom dashboard ?

It allows a user to customize the network and compute related security findings and occurences and display them across a variety of cards and graphs. 

Findings (ex - server is infected with malware, container has vulnerabilities etc) and its related metadata are exposed via APIs and are [Grafeas](https://grafeas.io/) inspired.
You can use the findings API to :
  - Register a new finding types.
  - Map finding types to UI cards using meta data.
  - Record occurrences of findings as KPIs and events.
  
One can feed a wide variety of data to Grafeas endpoint and organize them under logical tiles in a custom dashboard.

# How to use custom dashboard?

The dashboard has 2 sections: Network and Compute. You can feed security related data to the respective sections by posting relevant payloads as discussed below to the grafeas [endpoint](http://grafeas.ng.bluemix.net/v1alpha1/) . Find the swagger doc  [here](http://grafeas.ng.bluemix.net/ui/).

Let us assume we have a cluster created on the IBM container service called `cloudkingdom` which hosts one of your applications. One 
of the pods in that cluster is approaching external servers and sending them data in volumes that exceed that pod’s normal behavior.
We want to capture the instances of this behavior and show in the dashboard.

To achieve this we start by capturing the findings by posting the below payloads-
1. Create a project via the folloing CURL request -

Request:

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: <iam-token>'\
-d '{ "id": "my-security-advisor", "name": "my-security-advisor", "shared": false }'\
'https://grafeas.ng.bluemix.net/v1alpha1/projects'
```

Response:
```{
  "id": "my-security-advisor",
  "name": "projects/my-security-advisor",
  "shared": false
}
```

Note the id in the response which is used in the next step to target that project in grapheas endpoint .

2. We create a `note` via the following CURL request -
    
Request:
```bash
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' \
--header 'Authorization: <iam-token>' \
 -d '{
   "kind": "FINDING",
   "id": "notes-2",
   "reported_by": {
       "id": "outlier",
       "title": "Security Advisor"
   },
   "finding":
       {
           "severity":
               "HIGH",
           "next_steps":
               [
                   {
                       "title": "Investigate which process are running in your cluster. If you suspect one of your pods was hacked, restart it, and look for image vulnerabilities"
                   }]
       }
   ,
   "short_description": "One of the pods in your cluster appears to be leaking an excessive amount of data",
   "long_description": "One of the pods in your cluster is approaching external servers and sending them data in volumes that exceed that pod’s normal behavior"
}' 'https://grafeas.ng.bluemix.net/v1alpha1/projects/my-security-advisor/notes'
```

Response:
```
 {
  "create_time": "2018-03-14T12:09:31.442042Z",
  "create_timestamp": 1521029371.442042,
  "finding": {
    "next_steps": [
      {
        "title": "Investigate which process are running in your cluster. If you suspect one of your pods was hacked, restart it, and look for image vulnerabilities"
      }
    ],
    "severity": "HIGH"
  },
  "id": "notes-2",
  "kind": "FINDING",
  "long_description": "One of the pods in your cluster is approaching external servers and sending them data in volumes that exceed that pod\u2019s normal behavior",
  "name": "projects/my-security-advisor/notes/notes-2",
  "project_doc_id": "2436eb67dafff1627d2fb3d92bda7fcd/projects/my-security-advisor",
  "project_id": "my-security-advisor",
  "reported_by": {
    "id": "outlier",
    "title": "Security Advisor"
  },
  "shared": true,
  "short_description": "One of the pods in your cluster appears to be leaking an excessive amount of data",
  "update_time": "2018-03-14T12:09:31.442042Z",
  "update_timestamp": 1521029371.442042,
  "update_week_date": "2018-W11-3"
}
```
Note down the note id (i.e "note-2") which is used in the next step to capture occurences.

3. Next we capture the `occurences` of that finding . Replace "<account-id>" under "context" with your account-id .

Request 

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: <iam-token>' \
 -d '{
   "kind": "FINDING",
   "id": "occurrence2",
   "note_name": "projects/my-security-advisor/notes/notes-2",

   "context": {
       "region": "dal10",
       "account_id": "<account-id>",
       "resource_name": "cloudkingdom-pod",
       "resource_type": "Pod",
       "service_crn": "crn:v1:staging:public:containers-kubernetes:dal10:a/2436eb67dafff1627d2fb3d92bda7fcd:39438df3496a49e8aa39eb556ab15b0e::",
       "service_name": "Kubernetes Cluster"
   },
   "finding": {
       "certainty": "HIGH",
       "network": {
           "direction": "Outbound",
           "protocol": "Ethernet/IPv4/TCP"
       },
       "data_transferred": {
           "client_bytes": 983412
       }
   }
}' 'https://grafeas.ng.bluemix.net/v1alpha1/projects/my-security-advisor/occurrences'

```

Response

```
{
  "context": {
    "account_id": "<account_id>",
    "region": "dal10",
    "resource_name": "cloudkingdom-pod",
    "resource_type": "Pod",
    "service_crn": "crn:v1:staging:public:containers-kubernetes:dal10:a/2436eb67dafff1627d2fb3d92bda7fcd:39438df3496a49e8aa39eb556ab15b0e::",
    "service_name": "Kubernetes Cluster"
  },
  "create_time": "2018-03-14T12:10:43.446982Z",
  "create_timestamp": 1521029443.446982,
  "finding": {
    "certainty": "high",
    "data_transferred": {
      "client_bytes": 983412
    },
    "network": {
      "direction": "Outbound",
      "protocol": "Ethernet/IPv4/TCP"
    },
    "next_steps": [
      {
        "title": "Investigate which process are running in your cluster. If you suspect one of your pods was hacked, restart it, and look for image vulnerabilities"
      }
    ],
    "severity": "high"
  },
  "id": "occurrence2",
  "kind": "FINDING",
  "long_description": "One of the pods in your cluster is approaching external servers and sending them data in volumes that exceed that pod\u2019s normal behavior",
  "name": "projects/my-security-advisor/occurrences/occurrence2",
  "note_doc_id": "2436eb67dafff1627d2fb3d92bda7fcd/projects/my-security-advisor/notes/notes-2",
  "note_name": "projects/my-security-advisor/notes/notes-2",
  "project_doc_id": "2436eb67dafff1627d2fb3d92bda7fcd/projects/my-security-advisor",
  "project_id": "my-security-advisor",
  "reported_by": {
    "id": "outlier",
    "title": "Security Advisor"
  },
  "short_description": "One of the pods in your cluster appears to be leaking an excessive amount of data",
  "update_time": "2018-03-14T12:10:43.446982Z",
  "update_timestamp": 1521029443.446982,
  "update_week_date": "2018-W11-3"
}
```

4. We create a card to show the findings which we have captured for "notes-2" based on the above occurences .

Request 

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: <iam-token>' \
 -d '{ 
   "kind": "CARD",
   "id": "data-leakage-card",
   "short_description": "Data Leakage",
   "long_description": "Data Leakage card",
   "shared": false,

   "card": {
       "section": "Network",
       "title": "Data Leakage",
       "finding_note_names": [
           "projects/my-security-advisor/notes/notes-2"
       ],
       "elements": [
           {
               "kind": "NUMERIC",
               "text": "Excessive data",
               "value_type": {
                   "kind": "FINDING_COUNT",
                   "finding_note_names": [
                       "projects/my-security-advisor/notes/notes-2"
                   ]
               }
           },
           {
               "kind": "TIME_SERIES",
               "text": "Dala Leakage History",
               "default_interval": "1d",
               "default_time_range": "1w",
               "value_types": [
                   {
                       "kind": "FINDING_COUNT",
                       "finding_note_names": [
                           "projects/my-security-advisor/notes/notes-2"
                       ],
                       "text": "Excessive"
                   }
               ]
           }
       ]
   }
 }' 'https://grafeas.ng.bluemix.net/v1alpha1/projects/my-security-advisor/notes'
```

Response 

```
{
  "card": {
    "elements": [
      {
        "kind": "NUMERIC",
        "text": "Excessive data",
        "value_type": {
          "finding_note_names": [
            "projects/my-security-advisor/notes/notes-2"
          ],
          "kind": "FINDING_COUNT"
        }
      },
      {
        "default_interval": "1d",
        "default_time_range": "1w",
        "kind": "TIME_SERIES",
        "text": "Dala Leakage History",
        "value_types": [
          {
            "finding_note_names": [
              "projects/my-security-advisor/notes/notes-2"
            ],
            "kind": "FINDING_COUNT",
            "text": "Excessive"
          }
        ]
      }
    ],
    "finding_note_names": [
      "projects/my-security-advisor/notes/notes-2"
    ],
    "section": "Network",
    "title": "Data Leakage"
  },
  "create_time": "2018-03-14T12:09:04.366685Z",
  "create_timestamp": 1521029344.366685,
  "id": "data-leakage-card",
  "kind": "CARD",
  "long_description": "Data Leakage card",
  "name": "projects/my-security-advisor/notes/data-leakage-card",
  "project_doc_id": "2436eb67dafff1627d2fb3d92bda7fcd/projects/my-security-advisor",
  "project_id": "my-security-advisor",
  "shared": false,
  "short_description": "Data Leakage",
  "update_time": "2018-03-14T12:09:04.366685Z",
  "update_timestamp": 1521029344.366685,
  "update_week_date": "2018-W11-3"
}

```

To verify go to [dashboard] (https://console.ng.bluemix.net/security/advisor/#!/dashboard) , click on custom dashboard link .

