# ARGOCD

Configure ArgoCD rbac default policies.

```
oc edit argocd openshift-gitops -n openshift-gitops
```

```yaml
  rbac:
    policy: |
      g, system:cluster-admins, role:admin
      g, cluster-admins, role:admin
      g, argocd-admins, role:admin
```

```
oc edit cm argocd-rbac-cm -n openshift-gitops
```

```yaml
policy.default: ""
```

# TEKTON

Create secret for webhook and for registry access.

```
oc create secret generic pipeline-trigger-secret --from-literal=secretToken=XXX -n <namespace>
oc apply -f quay-secret.yaml -n <namespace>
oc secret link pipeline quay-secret --for=pull,mount -n <namespace>
```

# RBAC

Don't allow all users to create projects.

```
oc adm policy remove-cluster-role-from-group self-provisioner system:authenticated:oauth
```