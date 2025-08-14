<!-- markdownlint-disable MD033 MD041 -->
<div align="center">

<!-- markdownlint-disable MD033 -->
<img src="https://raw.githubusercontent.com/argoproj/argo-cd/master/docs/assets/argo.png" align="center"/>

### Ledger's Continuous Delivery Standard

... managed with ArgoCD :robot:

</div>

## :book:&nbsp; Overview

This directory contains ArgoCDs deployment manifests, that manage clusters resources in a GitOps way.

## :scroll:&nbsp; How to bootsrap

As ArgoCD deployment will be managed by itself, the first installation will need separate manuals tasks to be run once.

1. Log into the kubernetes cluster *<cluster_name>*
2. Create argocd namespace `kubectl create namespace argocd`
3. Create the sops secret `cat < AGE_FILE > | kubectl create secret generic sops-age --namespace=argocd --from-file=keys.txt=/dev/stdin`
4. Install ArgoCD `kubectl apply -k ./deploy/<cluster_name>/argocd`
5. Install the ArgoCD CLI `brew install argocd argocd/argo-cd` 
6. Get the admin account password `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`
7. Use the ArgoCD CLI to change the default password `argocd login <ARGOCD_SERVER_URL>` then `argocd account update-password`
8. Register the ArgoCD internal project to the cluster `kubectl apply -f deploy/common/argocd/projects/internal.yaml`
9. Register the ArgoCD application to the cluster `kubectl apply -f deploy/<cluster_name>/argocd/argocd-application.yaml`
10. Register the common application to the cluster `kubectl apply -f deploy/common/argocd-application.yaml`
11. Register app-of-apps `kubectl apply -f deploy/<cluster_name>/applications/app-of-apps.yaml`

## :scroll:&nbsp; How to add resources

## :scroll:&nbsp; How to update ArgoCD instances
