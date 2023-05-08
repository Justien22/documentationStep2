---
uid: VFDE_DataMiner_Footprint_Overview
---

# Overview

Vodafone is hosting the entire footprint in a virtualized environment. This means that all nodes (DataMiner, Cassandra & Elasticsearch) are running on VM guest images.
There are currently 3 different datacenter sites (Frankfurt, Kerpen & Munich ) but Munich is actively being decommissioned with end of 2023 as due date.
We've already completed migrating the DataMiner footprint from Munich to Kerpen. This leaves only a subset of the equipment under monitoring still at the datacenter in Munich.
All DataMiner footprint related nodes are currently hosted both Frankfurt and Kerpen datacenters.


# Georedundancy

The Frankfurt and Kerpen datacenters are configured in such a way that they provide georedundancy to the global infrastructure. Each individual datacenter also provides device level redundancy as well.
This means that a specific service signal typically flows twice in each datacenter. The end result of this is typically considered as quadrupal redundancy for a specific service signal flow.


# Production DMS Environment

The vodafone production environment currently exists out of 8 DataMiner nodes ( 4 in Frankfurt DC & 4 in Kerpen DC) which together form the operational production cluster.
It's configured to have one local database per cluster and has Search and Indexing enabled as well as an active DataMiner Cloud connection.

## DataMiner Cluster Nodes

8 production DataMiner agents, 4 located in each datacenter, configured as one DataMiner cluster.

|Hostname |Datacenter |IP Address|
|--------------------------|-------------|---------------|
|f-brei-dma-1              |Frankfurt    |10.252.51.1    |
|f-brei-dma-2              |Frankfurt    |10.252.51.2    |
|f-brei-dma-3              |Frankfurt    |10.252.51.3    |
|f-brei-dma-4              |Frankfurt    |10.252.51.4    |
|bm-mich-dma-1             |Kerpen       |10.253.51.1    |
|bm-mich-dma-2             |Kerpen       |10.253.51.2    |
|bm-mich-dma-3             |Kerpen       |10.253.51.3    |
|bm-mich-dma-4             |Kerpen       |10.253.51.4    |


DataMiner Node VM guest specification:

- OS: Windows Server 2019 Datacenter Edition
- CPU: 16 virtual cores
- RAM: 64 GB
- DISK: 1x 160 GB

## Cassandra Cluster Nodes

Configured as a dual datacenter cluster configuration where we have 3 nodes in both datacenters.

|Hostname |Datacenter |IP Address|
|--------------------------|-------------|---------------|
|f-brei-dma-db-prod-vm-1   |Frankfurt    |10.252.51.81   |
|f-brei-dma-db-prod-vm-2   |Frankfurt    |10.252.51.82   |
|f-brei-dma-db-prod-vm-3   |Frankfurt    |10.252.51.83   |
|bm-mich-dma-db-prod-vm-1  |Kerpen       |10.253.51.81   |
|bm-mich-dma-db-prod-vm-3  |Kerpen       |10.253.51.83   |
|bm-mich-dma-db-prod-vm-4  |Kerpen       |10.253.51.84   |


Cassandra Node VM guest specification:

- OS: Linux CENTOS 4.18
- CPU: 8 virtual cores
- RAM: 32 GB
- DISK: 1x 36 GB + 1x 320 GB

## Elasticsearch Clusters

Configured as 2 standalone Elasticsearch clusters, one in each datacenter.


Elastic Node VM guest specification:

- OS: Linux CENTOS 4.18
- CPU: 8 virtual cores
- RAM: 32 GB
- DISK: 1x 36 GB + 1x 320 GB


### Frankfurt cluster

|Hostname |Datacenter |IP Address|
|--------------------------|-------------|---------------|
|f-brei-dma-es-vm-1        |Frankfurt    |10.252.51.65   |
|f-brei-dma-es-vm-2        |Frankfurt    |10.252.51.66   |
|f-brei-dma-es-vm-3        |Frankfurt    |10.252.51.67   |

### Kerpen cluster

|Hostname |Datacenter |IP Address|
|--------------------------|-------------|---------------|
|bm-mich-dma-es-vm-1       |Kerpen       |10.253.51.65   |
|bm-mich-dma-es-vm-2       |Kerpen       |10.253.51.66   |
|bm-mich-dma-es-vm-3       |Kerpen       |10.253.51.67   |


# Preproduction DMS Environment

The vodafone preproduction environment currently exists out of 2 DataMiner nodes ( 1 in Frankfurt DC & 1 in Kerpen DC) which together form the DMS cluster.
The DataMiner agent in Frankfurt has been configured as a 1+1 failover pair.
The DMS is configured to have one local database per DMA and has Search and Indexing enabled as well as an active DataMiner Cloud connection.

## DataMiner Cluster Nodes

2 préproduction DataMiner agents, 1 located in each datacenter, configured as one DataMiner cluster.
The DataMiner agent in Frankfurt has been configured as 1+1 failover pair.
The DMS has been configured as local database per DMA. In this case, the Cassandra local database is hosted locally on the DataMiner node.

|Hostname |Datacenter |IP Address|
|-----------------------------|-------------|----------------|
|f-brei-dma-pp-1              |Frankfurt    |10.252.51.31    |
|f-brei-dma-pp-2              |Frankfurt    |10.252.51.32    |
|bm-mich-dma-pp-1             |Kerpen       |10.253.51.31    |


DataMiner Node VM guest specification:

- OS: Windows Server 2019 Datacenter Edition
- CPU: 6 virtual cores
- RAM: 32 GB
- DISK: 1x 60 GB + 1x 310 GB

## Elasticsearch Cluster

Configured as a single Elasticsearch cluster for the DMS. Hosted in the Frankfurt datacenter.

|Hostname |Datacenter |IP Address|
|--------------------------|-------------|---------------|
|f-brei-dma-es-vm-1        |Frankfurt    |10.252.51.96   |
|f-brei-dma-es-vm-2        |Frankfurt    |10.252.51.97   |
|f-brei-dma-es-vm-3        |Frankfurt    |10.252.51.98   |


Elastic Node VM guest specification:

- OS: Linux CENTOS 4.18
- CPU: 8 virtual cores
- RAM: 32 GB
- DISK: 1x 36 GB + 1x 320 GB

# Staging DMS Environment

The Vodafone staging environment currently exists out of a single DataMiner node ( 1 in Frankfurt DC ) which form the DMS cluster.
The DataMiner agent has been configured as a 1+1 failover pair.
The DMS is configured to have one local database per DMA and has Search and Indexing enabled as well as an active DataMiner Cloud connection.

## DataMiner Cluster Nodes

A single staging DataMiner agent, located in Frankfurt datacenter, configured as one DataMiner cluster.
The DataMiner agent in Frankfurt has been configured as 1+1 failover pair.
The DMS has been configured as local database per DMA. In this case, the Cassandra local database as well as Elasticsearch database are hosted locally on the DataMiner node.

|Hostname |Datacenter |IP Address|
|-----------------------------|-------------|----------------|
|f-brei-dma-pp3               |Frankfurt    |10.252.51.33    |
|f-brei-dma-pp4               |Frankfurt    |10.252.51.34    |


DataMiner Node VM guest specification:

- OS: Windows Server 2019 Datacenter Edition
- CPU: 6 virtual cores
- RAM: 32 GB
- DISK: 1x 60 GB + 1x 310 GB
