---
title: "Migrating KEDA Custom Resource Definitions (CRDs) and ScaledObjects API version
"
date: 2023-04-06T09:03:20-04:00
draft: false
---
 
KEDA (Kubernetes-based Event Driven Autoscaling) is an open-source project that provides event-driven autoscaling for Kubernetes workloads. As KEDA evolves, sometimes it's necessary to migrate the Custom Resource Definitions (CRDs) and ScaledObjects used by KEDA to enable new features or changes. This guide provides step-by-step instructions for migrating KEDA CRDs and ScaledObjects to a new API version.

## Prerequisites
Before migrating KEDA CRDs and ScaledObjects, ensure that you have:

- A Kubernetes cluster with KEDA installed
- Access to the Kubernetes manifests or Helm chart for KEDA installation
- Understanding of the differences between the current and the new API versions.

### Steps
1. Backup the current KEDA CRDs data by running the following command:
    ```bash
    kubectl get crd keda.k8s.io -o yaml > keda-crd-backup.yaml
    ```
    This command saves the current KEDA CRDs to a file named `keda-crd-backup.yaml`.
1. Backup the current ScaledObjects data by running the following command:
    ```bash
    kubectl get scaledobject.keda.io --all-namespaces -o yaml > keda-scaledobject-backup.yaml
    ```
    This command saves the current KEDA ScaledObjects to a file named `keda-scaledobject-backup.yaml`.
1. Open the Kubernetes manifest or Helm chart file that contains the KEDA ScaledObjects to be migrated.
1. Find the API version of the ScaledObjects in the file and update the API version to `keda.sh/v1Alpha`
1. Deploy the updated Kubernetes manifest or Helm chart
1. Verify that the new CRDs and ScaledObjects have been created by running the following command:
    ```bash
    kubectl get scaledobject.keda.sh --all-namespaces
    ```
    These commands list all KEDA ScaledObjects across all namespaces, respectively. Confirm that the ScaledObjects listed have the new API version.
1. Delete the old CRDs and ScaledObjects by running the following command:
    ```bash
    kubectl delete -f keda-crd-backup.yaml
    kubectl delete -f keda-scaledobject-backup.yaml
    ```
Congratulations! You've successfully migrated KEDA CRDs and ScaledObjects to a new API version.