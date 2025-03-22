# Understanding Pod Scheduling Behavior 🎭

## 📌 **Introduction**
In OpenShift, **Pod Scheduling** determines how pods are placed on worker nodes.  
The **Kubernetes Scheduler** uses various factors to decide pod placement, such as:
- **Resource availability** (CPU, Memory)  
- **Affinity & Anti-affinity rules**  
- **Taints and tolerations**  
- **Node selectors**  

---

## 🚀 **Pod Scheduling Components**

- **Scheduler** → Assigns pods to nodes based on constraints.  
- **Node Affinity** → Specifies which nodes a pod can run on.  
- **Taints and Tolerations** → Prevent or allow pods to run on certain nodes.  

---

## ⚙️ **Pod Scheduling Rules**

### 1️⃣ **Node Selector**

- Schedule pods on specific nodes using labels.

```bash
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
spec:
  nodeSelector:
    environment: production
  containers:
    - name: web
      image: nginx
```

👉 Apply the pod:

```bash
oc apply -f web-pod.yaml
```
---
2️⃣ Node Affinity

Use affinity rules to control pod placement.

```bash
apiVersion: v1
kind: Pod
metadata:
  name: affinity-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: environment
                operator: In
                values:
                  - production
  containers:
    - name: nginx
      image: nginx
```
---
👉 Apply the pod:

```bash
oc apply -f affinity-pod.yaml
```
---
3️⃣ Taints and Tolerations

Prevent certain pods from running on specific nodes.

# Add a taint to a node

```bash
oc adm taint nodes <node-name> key=value:NoSchedule
```
    
# Add tolerations to pods:

```bash
apiVersion: v1
kind: Pod
metadata:
  name: toleration-pod
spec:
  tolerations:
    - key: "key"
      operator: "Equal"
      value: "value"
      effect: "NoSchedule"
  containers:
    - name: nginx
      image: nginx
```

👉 Apply the pod:

```bash
oc apply -f toleration-pod.yaml
```

✅ Commands Summary
--

1️⃣ Apply Pod with Node Selector

```bash
oc apply -f <pod-file>.yaml
```

2️⃣ Add Taint to Node

```bash
oc adm taint nodes <node-name> key=value:NoSchedule
```
3️⃣ View Node Labels

```bash
oc get nodes --show-labels
```
