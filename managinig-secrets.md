### ✅  Managing Sensitive Information with Secrets 🔑

## 📌 **Introduction**
In OpenShift, **Secrets** are used to store and manage sensitive information securely, such as:
- API keys  
- Passwords  
- SSH keys  
- Certificates  

By using Secrets, you can avoid hard-coding sensitive data directly into the application or configuration files.

---

## 🚀 **Creating Secrets**

### 1️⃣ **Generic Secret**

```bash
oc create secret generic <secret-name> \
    --from-literal=username=admin \
    --from-literal=password=supersecret
```

### 2️⃣ **Secret from a File**

```bash
oc create secret generic db-credentials \
    --from-file=./db-user.txt \
    --from-file=./db-pass.txt
```

---

## 🔥 **Using Secrets in Applications**

### 1️⃣ **Mounting as Environment Variables**

You can use Secrets as environment variables in your application:

```yaml
env:
  - name: DB_USER
    valueFrom:
      secretKeyRef:
        name: db-credentials
        key: username
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: db-credentials
        key: password
```

### 2️⃣ **Mounting as Volumes**

You can mount Secrets as a volume in your pods:

```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: my-app-secret
```

---

## 🔐 **Security Tips**

```bash
# Avoid storing secrets in Git repositories
# Use 'oc extract' to view the secrets in a readable format
# Regularly rotate and update secrets
```

---

## ✅ **Commands Summary**

### 1️⃣ **Create a Secret**
```bash
oc create secret → Create a secret
```

### 2️⃣ **List Secrets**
```bash
oc get secrets → List secrets
```

### 3️⃣ **View Secret Details**
```bash
oc describe secret <name> → View secret details
```

### 4️⃣ **Extract and View Secret Data**
```bash
oc extract secret/<name> → Extract and view secret data
```


