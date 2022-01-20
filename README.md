# application-argocd
<p align="left">
<img src="https://img.shields.io/badge/redhat-CC0000?style=for-the-badge&logo=redhat&logoColor=white" alt="Redhat">
<img src="https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white" alt="kubernetes">
<img src="https://argo-cd.readthedocs.io/en/stable/assets/status-badge-healthy-synced.png" alt="ArgoCD">

</p>

GitOps scenario &amp; workshop manifests. Currently used for the [GitOps Courses DevNation](https://developers.redhat.com/courses/gitops/getting-started-argocd-and-openshift-gitops-operator)

#Install Red Hat OpenShift GitOps

```bash
oc get pods -n openshift-gitops
```

#Connecting to ArgoCD
Now that you've verified that Argo CD is up and running, let's explore how to access and manage Argo CD.

#Connecting to the Argo CD Server
Part of the setup of this lab connects you to the Argo CD instance via CLI and UI. Let's find the URL for the ArgoCD API Server:

```bash
oc get routes -n openshift-gitops | grep openshift-gitops-server | awk '{print $2}'
```

```bash
kubectl -n default get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

To login from the terminal, execute the following (replace $ARGOCD_SERVER_URL with the above URL):

```bash
argocd login $ARGOCD_SERVER_URL
```

Let's come back to the terminal. Verify that you're connected to the Argo CD API server by running the following:

```bash
argocd cluster list
```

This output lists the clusters that Argo CD manages. In this case in-cluster in the NAME field signifies that Argo CD is managing the cluster it's installed on.

To enable bash completion, run the following command:

```bash
source <(argocd completion bash)
```

```bash
ls ~/.argocd/config
```

#Create application

```bash
kubectl config get-contexts -o name
```

```bash
kubectl apply -f https://raw.githubusercontent.com/maximilianoPizarro/application-argocd/main/bgd-app.yaml
```

#Update application

```bash
argocd app sync bgd-app
```
