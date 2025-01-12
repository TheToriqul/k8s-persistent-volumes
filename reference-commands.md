# Kubernetes Storage Management Command Reference Guide

### Project Content Table
- [Basic Storage Operations](#basic-storage-operations)
- [Lab Exercises](#lab-exercises)
- [Advanced Volume Management](#advanced-volume-management)
- [StatefulSet Operations](#statefulset-operations)
- [Snapshot Operations](#snapshot-operations)
- [Monitoring and Maintenance](#monitoring-and-maintenance)

> **Author**: [Md Toriqul Islam](https://linkedin.com/in/thetoriqul)  
> **Description**: Comprehensive command reference for Kubernetes storage management  
> **Learning Focus**: Mastering persistent storage operations in Kubernetes  
> **Note**: Always understand command implications before execution

## Basic Storage Operations

### Step 1: Storage Class Management
```bash
# Create the standard storage class
kubectl apply -f storage-class.yaml

# List available storage classes
kubectl get storageclass

# Verify storage class
kubectl describe storageclass standard
```

### Step 2: Create and Verify PV
```bash
# Create persistent volume
kubectl apply -f persistent-volume.yaml

# List all persistent volumes
kubectl get pv

# Get detailed PV information
kubectl describe pv task-pv

# Check PV status (should show Available)
kubectl get pv task-pv -o jsonpath='{.status.phase}'
```

### Step 3: Create and Verify PVC
```bash
# Create persistent volume claim
kubectl apply -f persistent-volume-claim.yaml

# List all PVCs
kubectl get pvc

# Check PVC details
kubectl describe pvc task-pvc

# Monitor PVC status (should show Bound)
kubectl get pvc task-pvc -o jsonpath='{.status.phase}'
```

## Lab Exercises

### Basic PV/PVC Setup
```bash
# Create PV with path /data/db
kubectl create -f pv.yaml

# Verify PV creation (should show Available)
kubectl get pv

# Create PVC requesting 256Mi
kubectl create -f pvc.yaml

# Check PVC status
kubectl get pvc

# Get detailed PVC information
kubectl describe pvc db-pvc

# Check Used by attribute (should show <none> if not mounted)
kubectl get pvc db-pvc -o jsonpath='{.status.phase}'
```

### Pod Volume Mounting
```bash
# Deploy pod with mounted volume
kubectl apply -f pod-with-pvc.yaml

# Verify pod creation
kubectl get pods task-pod

# Check volume mounting
kubectl describe pod task-pod | grep -A 5 Volumes

# Verify mount points
kubectl exec -it task-pod -- df -h

# Check mounted directory permissions
kubectl exec -it task-pod -- ls -la /usr/share/nginx/html
```

## Advanced Volume Management

### Dynamic Provisioning
```bash
# Create storage class for dynamic provisioning
kubectl apply -f dynamic-pv-storage-class.yaml

# Create PVC with dynamic provisioning
kubectl apply -f dynamic-pvc.yaml

# Verify dynamic PVC creation
kubectl get pvc dynamic-pvc

# Check auto-provisioned PV
kubectl get pv
```

## StatefulSet Operations
```bash
# Deploy StatefulSet with PVC
kubectl apply -f statefulset-with-pvc.yaml

# Check StatefulSet status
kubectl get statefulset webapp

# Verify PVC creation for each replica
kubectl get pvc -l app=nginx

# Check pod status and volume mounting
kubectl get pods -l app=nginx
kubectl describe pods -l app=nginx | grep -A 5 Volumes
```

## Snapshot Operations
```bash
# Create snapshot class
kubectl apply -f volume-snapshot-class.yaml

# Create volume snapshot
kubectl apply -f volume-snapshot.yaml

# List snapshots
kubectl get volumesnapshot

# Check snapshot details
kubectl describe volumesnapshot task-snapshot

# Create PVC from snapshot
kubectl apply -f restore-pvc-from-snapshot.yaml
```

## Monitoring and Maintenance

### Health Checks
```bash
# Check all storage resources
kubectl get pv,pvc,pods --all-namespaces

# Monitor pod events
kubectl get events --field-selector involvedObject.kind=Pod

# Check storage provisioner status
kubectl get pods -n kube-system | grep provisioner
```

### Storage Cleanup
```bash
# Delete pod
kubectl delete pod task-pod

# Delete PVC (verify data is backed up first)
kubectl delete pvc task-pvc

# Delete PV
kubectl delete pv task-pv

# Delete storage class (only if no PVs are using it)
kubectl delete storageclass standard
```

## Learning Notes

1. Always verify PV and PVC binding before using in pods
2. Check storage class configuration and provisioner availability
3. Monitor pod events for volume mounting issues
4. Use appropriate access modes based on requirements
5. Understand reclaim policies and their implications

---

> 💡 **Best Practice**: Create resources in order: StorageClass → PV → PVC → Pod/StatefulSet

> ⚠️ **Warning**: Never delete PVs that are in use by PVCs

> 📝 **Note**: Regular backup of persistent data is crucial