# Resource Limits & Requests for Applications 💻

## 📌 **Introduction**
In OpenShift, **Resource Limits & Requests** help manage the CPU and memory usage of your applications.  
They prevent resource overuse and ensure fair distribution across nodes.

---

## 🚀 **Key Concepts**

- **Requests** → The minimum CPU and memory a pod requires.  
- **Limits** → The maximum CPU and memory a pod can use.  
- **QoS Classes** → Determines how resources are allocated:
  - **Guaranteed** → Requests = Limits (highest priority)  
  - **Burstable** → Requests < Limits (medium priority)  
  - **BestEffort** → No requests or limits defined (lowest priority)  

---

## ⚙️ **Defining Resource Limits**

### 1️⃣ **Set CPU and Memory Requests/Limits**

```bash
apiVersion: v1
kind: Pod
metadata:
  name: resource-pod
spec:
  containers:
    - name: app
      image: nginx
      resources:
        requests:
          memory: "512Mi"
          cpu: "250m"
        limits:
          memory: "1Gi"
          cpu: "500m"
```
---
👉 Apply the pod:

```bash
oc apply -f resource-pod.yaml
```

2️⃣ Verify Resource Usage

# Check pod resource usage
```bash
oc describe pod <pod-name>
```

3️⃣ Set Resource Quotas

```bash
apiVersion: v1
kind: ResourceQuota
metadata:
  name: mem-cpu-quota
spec:
  hard:
    requests.cpu: "2"
    requests.memory: "4Gi"
    limits.cpu: "4"
    limits.memory: "8Gi"
```
👉 Apply the quota:

```bash
oc apply -f mem-cpu-quota.yaml
```
✅ Commands Summary
---
1️⃣ Apply Pod with Resource Limits

```bash
oc apply -f <pod-file>.yaml
```

2️⃣ View Resource Usage

```bash
oc describe pod <pod-name>
```

3️⃣ Apply Resource Quota

```bash
oc apply -f <quota-file>.yaml
```
