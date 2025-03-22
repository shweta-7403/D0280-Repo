# Software-defined Networking (SDN) in OpenShift 🌐

## 📌 **Introduction**
In OpenShift, **Software-defined Networking (SDN)** provides a flexible and scalable way to manage network communication between pods, services, and external endpoints.  
It uses **OVN-Kubernetes** (default in OpenShift 4.x) or **OpenShift SDN** for networking.

---

## 🚀 **SDN Modes in OpenShift**

| Mode          | Description                                       |
|---------------|---------------------------------------------------|
| `networkpolicy` | Uses Kubernetes network policies for isolation.  |
| `multitenant`   | Isolates namespaces by default, but allows exceptions. |
| `subnet`        | All pods can communicate without restrictions. |

---

## 🔥 **SDN Components**

- **Open vSwitch (OVS)** → Provides Layer 2 and Layer 3 switching capabilities.  
- **OVN (Open Virtual Network)** → Handles routing, NAT, and distributed gateways.  
- **Kubernetes CNI (Container Network Interface)** → Manages pod networking.  

---

## ⚙️ **SDN Configuration**

### 1️⃣ **Check Current SDN Mode**
```bash
oc get network.operator cluster -o jsonpath='{.spec.defaultNetwork.type}'
```

2️⃣ Change SDN Mode

```bash
oc patch network.operator cluster -p '{"spec":{"defaultNetwork":{"type":"OpenShiftSDN"}}}' --type=merge
```
