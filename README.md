# openshift-gitops-example

GitOps scenario &amp; workshop manifests. Currently used for the [GitOps Courses DevNation](https://developers.redhat.com/courses/gitops/getting-started-argocd-and-openshift-gitops-operator)

#Install Red Hat GitOps Operator

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
oc extract secret/openshift-gitops-cluster -n openshift-gitops --to=-
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
oc apply -f https://raw.githubusercontent.com/maximilianoPizarro/openshift-gitops-examples/main/bgd-app.yaml
```

```bash
argocd app sync bgd-app
```