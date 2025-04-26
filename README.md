# Kubernetes Cluster Administration: RBAC

Role-Based Access Control (RBAC) is a crucial security mechanism in Kubernetes that allows you to define who can access what resources within your cluster.

## Core Components of Kubernetes RBAC

1. **Roles and ClusterRoles**: Define what actions can be performed on which resources
2. **RoleBindings and ClusterRoleBindings**: Connect users, groups, or service accounts to roles
3. **ServiceAccounts**: Identities for processes running in pods

## Key RBAC Concepts

### Roles vs ClusterRoles

- **Roles** are namespace-scoped (apply within a specific namespace)
- **ClusterRoles** are cluster-wide (apply across all namespaces)

### Example Role Definition

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

### Example RoleBinding

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

## Best Practices

1. **Principle of Least Privilege**: Grant only necessary permissions
2. **Use Groups**: Assign permissions to groups rather than individual users
3. **Regular Audits**: Review RBAC policies regularly
4. **Default Deny**: Start with no permissions and add as needed
5. **Namespace Isolation**: Use namespaces to separate environments and teams

## Common Commands

```bash
# List roles in a namespace
kubectl get roles -n <namespace>

# List cluster roles
kubectl get clusterroles

# Describe a specific role
kubectl describe role <role-name> -n <namespace>

# Check if a user can perform an action
kubectl auth can-i <verb> <resource> --as=<username>
```

Would you like me to delve deeper into any specific aspect of Kubernetes RBAC?
