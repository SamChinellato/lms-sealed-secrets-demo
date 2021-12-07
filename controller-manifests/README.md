# Sealed Secrets Controller

## Prerequisites

Install with kustomize:

    brew install kustomize

### Set the target namespace (optional)

The target namespace is set to: `sealed-secrets`, if you want to change it, run (from this directory):

    kustomize edit set namespace <another-namespace>

(You should see the namespace update in `kustomization.yaml`)

## Install

    kustomize build | oc apply -f -

See the pod:
```
oc get pods -n sealed-secrets
```
---