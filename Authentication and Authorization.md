# Authentication and Authorization in OpenShift

## 1. Configuring Identity Providers (OAuth, LDAP, etc.) 🔑
Authentication in OpenShift determines who a user is and how they can access the system. OpenShift supports multiple identity providers, including:

### 1.1 OAuth Authentication
- OpenShift uses **OAuth 2.0** for authentication by default.
- Users can log in using web-based authentication.
- OpenShift integrates with identity providers like GitHub, Google, and LDAP.

**Example: Configuring GitHub as an OAuth Provider**
```yaml
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  name: cluster
spec:
  identityProviders:
  - name: github
    mappingMethod: claim
    type: GitHub
    github:
      clientID: <your-client-id>
      clientSecret:
        name: github-secret
      organizations:
      - your-org-name
```
- The client ID and secret must be obtained from **GitHub Developer Settings**.

### 1.2 LDAP Authentication
- LDAP authentication allows integrating an enterprise directory service like **Active Directory**.
- Users authenticate against an external directory service.

**Example: Configuring LDAP Authentication**
```yaml
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  name: cluster
spec:
  identityProviders:
  - name: ldap
    mappingMethod: claim
    type: LDAP
    ldap:
      url: "ldap://ldap.example.com/ou=users,dc=example,dc=com?uid"
      insecure: false
      bindDN: "cn=admin,dc=example,dc=com"
      bindPassword:
        name: ldap-secret
```
- Users from the **LDAP directory** can log in using their credentials.

## 2. Role-Based Access Control (RBAC) 🏗️
RBAC controls what actions users can perform within OpenShift.

### 2.1 Key RBAC Components
| Component | Description |
|-----------|------------|
| **Rules** | Define allowed actions on objects |
| **Roles** | Collection of rules assigned to users |
| **RoleBindings** | Associate roles with users or groups |
| **ClusterRoles** | Roles that apply across all projects |
| **LocalRoles** | Roles scoped to a specific project |

### 2.2 Managing RBAC with CLI
**Assign a Cluster Role to a User:**
```sh
oc adm policy add-cluster-role-to-user cluster-admin user1
```
**Remove a Cluster Role from a User:**
```sh
oc adm policy remove-cluster-role-from-user cluster-admin user1
```
**Assign a Project Role to a User:**
```sh
oc policy add-role-to-user edit user1 -n project-name
```

## 3. User Permissions & Security Policies 📜
User permissions define what actions a user can perform in OpenShift.

### 3.1 Default User Roles
| Role | Description |
|------|------------|
| **admin** | Full project access |
| **basic-user** | Read access to the project |
| **cluster-admin** | Full cluster access |
| **edit** | Modify application resources |
| **view** | Read-only access |

### 3.2 Managing Security Policies
- OpenShift enforces **Security Context Constraints (SCCs)** to restrict container permissions.
- Default SCCs include **privileged**, **restricted**, and **anyuid**.

**View SCCs:**
```sh
oc get scc
```
**Modify SCCs:**
```sh
oc adm policy add-scc-to-user anyuid -z default -n my-project
```



