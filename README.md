# Splunk-Indexer-Cluster-Project-on-AWS-

Splunk Indexer Cluster Project on (AWS) — Complete Documentation



&#x20;                   ┌────────────────────┐

&#x20;                   │   Search Head      │

&#x20;                   │   (10.0.1.152)     │

&#x20;                   └────────┬───────────┘

&#x20;                            │ Forwarding (9997)

&#x20;        ┌───────────────────┼───────────────────┐

&#x20;        │                   │                   │

┌────────▼────────┐ ┌────────▼────────┐ ┌────────▼────────┐

│ Indexer Peer 1  │ │ Indexer Peer 2  │ │ Indexer Peer 3  │

│ 10.0.2.37       │ │ 10.0.2.111      │ │ 10.0.2.202      │

└────────┬────────┘ └────────┬────────┘ └────────┬────────┘

&#x20;        │                   │                   │

&#x20;        └────────── Cluster Manager ────────────┘

&#x20;                   (10.0.x.x)



**2. VPC Setup**





&#x20;Component      	 Value

&#x20;-------------- 	 -----------

&#x20;VPC CIDR       	 10.0.0.0/16

&#x20;Public Subnet  	 10.0.1.0/24

&#x20;Private Subnet 	 10.0.2.0/24



**3. Subnet Usage**



Instance:		Subnet:

Search Head		Public Subnet

Cluster Manager		Public Subnet

Peer Nodes		Private Subnet



