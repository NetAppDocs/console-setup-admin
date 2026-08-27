# ONTAP Guidance

Canonical source: https://docs.netapp.com/us-en/ontap/index.html

Use this reference only when a request involves ONTAP terminology or behavior that the target page and related repository content do not establish. Repository documentation remains the authority for NetApp Console (local deployment) behavior and integrations.

## Performance Rules

1. Read this guide only for ONTAP-related requests.
2. Retrieve only the narrowest canonical ONTAP page needed to verify a claim. Do not retrieve the ONTAP landing page or broad topic areas repeatedly.
3. Stop after verifying the required terminology or behavior. Do not research adjacent ONTAP features.
4. State uncertainty when a specific source does not support the proposed statement.

## Core Terminology

Use these terms consistently. Verify detailed behavior from the canonical ONTAP documentation when it affects the statement.

| Term | Use |
| --- | --- |
| Cluster | A group of ONTAP nodes managed as one system. |
| Storage VM (SVM) | A logical storage server that serves data. |
| Volume | A flexible container for data in an SVM. |
| LUN | A logical unit of storage used for SAN workloads. |
| Aggregate | The underlying storage pool that supplies capacity to volumes. |
| Snapshot copy | A point-in-time, read-only copy of a volume. |
| QoS | A policy that controls workload performance characteristics, such as IOPS or throughput limits. |
| FabricPool | ONTAP tiering that moves inactive data to cloud or object storage. |

## Topic Routing

| Need to verify | Canonical ONTAP topic |
| --- | --- |
| Volumes, aggregates, and storage efficiency | https://docs.netapp.com/us-en/ontap/volume-admin/index.html |
| NAS protocols and data access | https://docs.netapp.com/us-en/ontap/nas-management/index.html |
| SAN, LUNs, and host access | https://docs.netapp.com/us-en/ontap/san-management/index.html |
| Data protection and disaster recovery | https://docs.netapp.com/us-en/ontap/data-protection-disaster-recovery/index.html |
| Performance, events, and health | https://docs.netapp.com/us-en/ontap/event-performance-monitoring/index.html |
| Authentication and access control | https://docs.netapp.com/us-en/ontap/authentication-access-control/index.html |
| Security and encryption | https://docs.netapp.com/us-en/ontap/security-encryption/index.html |
| Object storage and FabricPool | https://docs.netapp.com/us-en/ontap/object-storage-management/index.html |

Do not use an ONTAP source alone to assert a NetApp Console (local deployment) workflow, interface, permission, integration, or automated behavior. Those claims require support from this repository.