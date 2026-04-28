# Splunk-Indexer-Cluster-Project-on-AWS-

Splunk Indexer Cluster Project on (AWS) — Complete Documentation



                ┌────────────────────┐

               │   Search Head      │

                   │   (10.0.1.152)     │


                   └────────┬───────────┘
                            │ Forwarding (9997)
     
  ┌───────────────────┼───────────────────┐

        │                   │                   │

┌────────▼────────┐ ┌────────▼────────┐ ┌────────▼────────┐

│ Indexer Peer 1  │ │ Indexer Peer 2  │ │ Indexer Peer 3  │

│ 10.0.2.37       │ │ 10.0.2.111      │ │ 10.0.2.202      │

└────────┬────────┘ └────────┬────────┘ └────────┬────────┘

      │                   │                   │

       └────────── Cluster Manager ────────────┘

                  (10.0.x.x)

2. VPC Setup**

Component      	 Value
-------------- 	 -----------

VPC CIDR       	 10.0.0.0/16

Public Subnet  	 10.0.1.0/24

Private Subnet 	 10.0.2.0/24
----------------------------------
3. Subnet Usage

Instance:		        Subnet:

Search Head		     Public Subnet

Cluster Manager	             Public Subnet

Peer Nodes		     Private Subnet

-------------------------------------------


4. Security Group Rules

Inbound Rules

Port	Purpose

22	SSH

8000	Splunk Web

8089	Management

9997	Forwarding

9887	Clustering

Source:

10.0.0.0/16

5. Indexer Cluster Configuration

Cluster Manager (server.conf)

[clustering]
mode = manager
replication_factor = 3
search_factor = 2
pass4SymmKey = MyPassword123
cluster_label = aws_cluster

Peer Nodes (server.conf)
[clustering]
mode = peer
manager_uri = https://<CLUSTER_MANAGER_IP>:8089
replication_port = 9887
pass4SymmKey = MyPassword123
cluster_label = aws_cluster

Enable Receiving Port (Peers)
splunk enable listen 9997 -auth admin:password

outputs.conf (Search Head)

[tcpout]
defaultGroup = idxcluster

[tcpout:idxcluster]
server = 10.0.2.37:9997,10.0.2.111:9997,10.0.2.202:9997
autoLB = true
forceTimebasedAutoLB = true

Index Creation
Created on Cluster Manager:

[aws_cluster_index]
homePath = $SPLUNK_DB/aws_cluster_index/db
coldPath = $SPLUNK_DB/aws_cluster_index/colddb
thawedPath = $SPLUNK_DB/aws_cluster_index/thaweddb


Data Ingestion

Used Search Head → Add Data
Uploaded app.log
Indexed into:
aws_cluster_index