# Verifying and Troubleshooting Cluster Health in OpenShift

## 1️⃣ OpenShift Installation Methods 🏗️

### **1.1 Installer-Provisioned Infrastructure (IPI)**
- **Fully automated installation**
- Requires cloud providers like AWS, Azure, or vSphere
- Installs all OpenShift components, including networking and storage
- Best for **quick deployments**

### **1.2 User-Provisioned Infrastructure (UPI)**
- **Manual installation method**
- Users configure infrastructure (networking, storage, etc.)
- Best for **custom deployments** or on-premise installations

### **1.3 Local Development Installations**
- **CodeReady Containers (CRC):** Runs OpenShift on a local machine
- **Minishift:** Lightweight OpenShift for development & testing

## 2️⃣ Troubleshooting OpenShift Clusters & Applications 🛠️

### **2.1 Cluster Health Check Commands**
#### Check overall cluster status:
```bash
oc get clusterversion
```

#### Check cluster nodes:
```bash
oc get nodes
```

#### Check pods in all namespaces:
```bash
oc get pods --all-namespaces
```

#### Check logs of a specific pod:
```bash
oc logs -f <pod-name> -n <namespace>
```

### **2.2 Common Cluster Issues & Fixes**
#### **1. Node Not Ready**
✅ **Check node status:**
```bash
oc describe node <node-name>
```
✅ **Check kubelet logs:**
```bash
journalctl -u kubelet -f
```
✅ **Restart services if needed:**
```bash
systemctl restart kubelet
```

#### **2. Pods Stuck in Pending State**
✅ **Check events for the pod:**
```bash
oc describe pod <pod-name> -n <namespace>
```
✅ **Check if sufficient resources are available:**
```bash
oc get nodes -o wide
```
✅ **Check if the scheduler is working:**
```bash
oc get events
```

#### **3. Network Issues**
✅ **Check network policies applied to the pod:**
```bash
oc get networkpolicy -n <namespace>
```
✅ **Check service endpoints:**
```bash
oc get endpoints -n <namespace>
```
✅ **Test connectivity using curl/ping:**
```bash
oc rsh <pod-name> curl <service-name>:<port>
```

### **2.3 Debugging OpenShift Applications**
#### **Check Deployment Status:**
```bash
oc get deployment -n <namespace>
```
#### **Manually Scale Up/Down a Deployment:**
```bash
oc scale deployment <deployment-name> --replicas=3 -n <namespace>
```
#### **Restart a Pod (By Deleting & Letting it Recreate Automatically):**
```bash
oc delete pod <pod-name> -n <namespace>
```

## 3️⃣ Introduction to OpenShift Dynamic Storage 💾

### **3.1 What is Dynamic Storage in OpenShift?**
- OpenShift supports **dynamic provisioning** of persistent storage.
- Storage is automatically allocated when a pod requests it.
- No need to manually create storage volumes.

### **3.2 Storage Classes in OpenShift**
#### List available storage classes:
```bash
oc get storageclass
```
#### Create a Persistent Volume Claim (PVC):
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
  namespace: my-project
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: standard
```
#### Apply the PVC:
```bash
oc apply -f my-pvc.yaml
```

### **3.3 Checking Storage Usage**
#### Get all Persistent Volume Claims (PVCs):
```bash
oc get pvc -n <namespace>
```
#### Describe a PVC:
```bash
oc describe pvc <pvc-name> -n <namespace>
```
#### Get Persistent Volumes (PVs):
```bash
oc get pv
```

---



