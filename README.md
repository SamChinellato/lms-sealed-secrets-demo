# Sealed Secrets Demo

This repository sets up a demo for sealed secrets.

## Prerequisites


* Install the `Openshift Pipeline` and `OpenShift GitOps` operators.

---

## Install

Install the sealed secrets controller. Do so [following the README in `controller-manifests`](./controller-manifests/README.md)

### ArgoCD Setup

#### Configure known_hosts
Log into Argo (using the route in `openshift-gitops`) and head to `Settings > Repository Certificates > ADD SSH KNOWN HOSTS`. Run the following and copy the output into the ArgoCD UI:
```
ssh-keyscan github.ibm.com
```
#### Add a Source Repository
Generate an ssh-key:
```
 ssh-keygen -t rsa -b 4096 -C <email>
```
Add the public key as a `Deploy key` to [this repo](https://github.ibm.com/itg-europe-appmod-devops-cop/postgresql-sample).

On the Argo UI, head to `Settings > Repositories > CONNECT REPO USING SSH` and paste the private key there. Add in the ssh clone url for [this repo](https://github.ibm.com/itg-europe-appmod-devops-cop/postgresql-sample). 

---

## Run Tekton Pipeline

Set the project to `sealed-secrets`
```
oc project sealed-secrets
```

Create the tasks:
```
oc apply -f ./tekton/base
```

Start the pipeline:
```
oc create -f ./tekton/yasrs-pipeline.yaml
```

You should see Tekton update [this repo](https://github.ibm.com/itg-europe-appmod-devops-cop/postgresql-sample). 

---

## Deploy Argo Application

Run the following to create a demo namespace, configure RBAC for the Openshift Gitops operator and deploy an ArgoCD:

```
oc apply -f ./gitops-config.yaml
```

Notice the application coming up in the `postgresql` namespace:

```
oc get all -n postgresql
```
> N.B. If you did not run the Tekton pipeline in the previous step, you may notice an `UnsealError` for the `SealedSecret` in the deployment. This is due to the `SealedSecret` being encrypted with a sealing key your Sealed Secrets controller is not aware of. This will be fixed by running the pipeline.