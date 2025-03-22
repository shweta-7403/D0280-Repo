### ✅ Application Security Context Constraints (SCCs) 🚧

## 📌 **Introduction**
In OpenShift, **Security Context Constraints (SCCs)** define the actions that a **pod** or container can perform.  
They control security-sensitive aspects like:
- Running as a specific user or group  
- Using privileged mode  
- Mounting host paths  
- Accessing network namespaces  

---

## 🚀 **Common SCCs in OpenShift**

| SCC Name       | Description                                      |
|----------------|--------------------------------------------------|
| `anyuid`       | Allows running as any UID, including root.       |
| `restricted`   | Ensures restricted access, non-root execution.   |
| `privileged`   | Grants privileged mode access.                   |
| `hostnetwork`  | Allows using the host network.                   |
| `nonroot`      | Requires running as a non-root user.             |

---

## 🔥 **Creating and Using SCCs**

### 1️⃣ **View Existing SCCs**

```bash
oc get scc
```

---

### 2️⃣ **Describe SCC**

```bash
oc describe scc <scc-name>
```

---

### 3️⃣ **Assign SCC to Service Account**

```bash
oc adm policy add-scc-to-user restricted -z <service-account-name>
```

---

### 4️⃣ **Sample SCC YAML**

```bash
apiVersion: security.openshift.io/v1
kind: SecurityContextConstraints
metadata:
  name: custom-scc
allowPrivilegedContainer: false
runAsUser:
  type: MustRunAsNonRoot
seLinuxContext:
  type: MustRunAs
fsGroup:
  type: MustRunAs
supplementalGroups:
  type: RunAsAny
```

👉 Apply the SCC:

```bash
oc apply -f custom-scc.yaml
```

---

## 🔐 **Best Practices**

```bash
# Use 'restricted' SCC for most workloads
# Only assign 'privileged' SCC when necessary
# Regularly audit SCCs using:
oc adm policy who-can use scc/<scc-name>
```

---

## ✅ **Commands Summary**

### 1️⃣ **List Available SCCs**
```bash
oc get scc
```

### 2️⃣ **View SCC Details**
```bash
oc describe scc <name>
```

### 3️⃣ **Assign SCC to User/Service Account**
```bash
oc adm policy add-scc-to-user restricted -z <service-account-name>
```

### 4️⃣ **Apply SCC from YAML**
```bash
oc apply -f <scc-file>
```

