### 📄 Exposing Applications for External Access 🚪

## 📌 **Introduction**
In OpenShift, you can expose your applications to **external users** by creating:
- **Routes** → Ingress layer that exposes services externally.  
- **Services** → Internal communication between pods.  
- **Load Balancers** → Exposes services externally via a cloud provider.  

---

## 🚀 **Methods for Exposing Applications**

### 1️⃣ **Using a Route**

- A **Route** exposes a service over HTTP/HTTPS externally.  

```bash
oc expose service <service-name> --name=<route-name>

```

👉 Verify the route:

```bash
oc get route <route-name> -o jsonpath='{.spec.host}'
```

2️⃣ Using a Load Balancer

A Load Balancer service type makes the application externally accessible via cloud provider.

       
```bash
oc expose deployment <deployment-name> --type=LoadBalancer --name=<service-name>
```

👉 Check the external IP:

```bash
oc get svc <service-name>
```

3️⃣ Using NodePort

NodePort exposes the application on a static port.

```bash
oc expose deployment <deployment-name> --type=NodePort --name=<service-name>
```

👉 Check the exposed port:
```bash
oc get svc <service-name> -o jsonpath='{.spec.ports[0].nodePort}'
```


✅ Commands Summary
---

1️⃣ Expose with Route

```bash
oc expose service <service-name> --name=<route-name>
```

2️⃣ Expose with Load Balancer

```bash
oc expose deployment <deployment-name> --type=LoadBalancer --name=<service-name>
```

3️⃣ Expose with NodePort

```bash
oc expose deployment <deployment-name> --type=NodePort --name=<service-name>
```
