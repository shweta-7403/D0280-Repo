### 📄 Scaling Applications for Performance Optimization 📈

## 📌 **Introduction**
In OpenShift, **scaling** allows you to dynamically adjust the number of pods in a deployment or replicaset.  
This ensures high availability and better performance during peak loads.

---

## 🚀 **Scaling Methods**

- **Manual Scaling** → Increase or decrease pod replicas manually.  
- **Horizontal Pod Autoscaler (HPA)** → Automatically scales pods based on CPU/memory usage.  
- **Vertical Pod Autoscaler (VPA)** → Adjusts the resource requests and limits automatically.  

---

## ⚙️ **Scaling Applications**

### 1️⃣ **Manual Scaling**

# Scale a deployment to 5 replicas
```bash

oc scale deployment <deployment-name> --replicas=5
```
2️⃣ Horizontal Pod Autoscaler (HPA)

# Create an HPA based on CPU usage
```bash
oc autoscale deployment <deployment-name> \
    --min=2 --max=10 --cpu-percent=70
```

👉 Check HPA status:

```bash
oc get hpa
```

3️⃣ Vertical Pod Autoscaler (VPA)

```bash
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: vpa-example
spec:
  targetRef:
    apiVersion: "apps/v1"
    kind: Deployment
    name: <deployment-name>
  updatePolicy:
    updateMode: "Auto"
```

👉 Apply the VPA:

```bash
oc apply -f vpa.yaml
```

✅ Commands Summary
---

1️⃣ Scale Deployment

```bash
oc scale deployment <name> --replicas=<num>
```

2️⃣ Create HPA

```bash
oc autoscale deployment <name> --min=2 --max=10 --cpu-percent=70
```

3️⃣ Apply VPA

```bash
oc apply -f vpa.yaml
```


```
