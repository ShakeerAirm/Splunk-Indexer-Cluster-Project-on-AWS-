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



