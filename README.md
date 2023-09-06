# ARGOCD
```oc edit argocd openshift-gitops -n openshift-gitops
  rbac:
    policy: |
      g, system:cluster-admins, role:admin
      g, cluster-admins, role:admin
      g, argocd-admins, role:admin
```

# TEKTON
```
oc create secret generic pipeline-trigger-secret --from-literal=secretToken=XXX -n springboot-dev
oc apply -f quay-secret.yaml -n springboot-dev
oc secret link pipeline quay-secret --for=pull,mount -n springboot-dev
```

# RBAC
```
oc adm policy remove-cluster-role-from-group self-provisioner system:authenticated:oauth
```