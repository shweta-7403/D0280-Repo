
### 📄 # Configuring Network Policies for Security 🔒

## 📌 **Introduction**
In OpenShift, **Network Policies** control how pods communicate with each other and with external networks.  
They allow you to **restrict** or **allow** traffic based on:  
- **Labels**  
- **Namespaces**  
- **Ports**  

---

## 🚀 **Creating Network Policies**

### 1️⃣ **Allowing Intra-namespace Communication**

```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-same-namespace
spec:
  podSelector: {}
  policyTypes:
    - Ingress
  ingress:
    - from:
        - podSelector: {}

```

👉 Apply the policy:

```bash
oc apply -f allow-same-namespace.yaml
```

2️⃣ Restricting External Access

```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: block-external-access
spec:
  podSelector: {}
  policyTypes:
    - Ingress
  ingress: []
```
---
👉 Apply the policy:

```bash
oc apply -f block-external-access.yaml
```
---

3️⃣ Allowing Specific Namespace Traffic

```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-namespace-access
spec:
  podSelector: {}
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              app: trusted
```
---
👉 Apply the policy:


```bash
oc apply -f allow-namespace-access.yaml
```
---

✅ Commands Summary
---

1️⃣ Apply a Network Policy

```bash
oc apply -f <network-policy-file>
```

2️⃣ List Network Policies

```
oc get networkpolicy
```

3️⃣ Delete a Network Policy

```
oc delete networkpolicy <policy-name>
```
