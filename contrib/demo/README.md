# KCP-OCM Demo (first draft)

The `demo` shows a prototype using `kcp` API server with `kcp-ocm` controller to demonstrate synergy between existing open-cluster-management concepts with KCP concept of "transparent multicluster"

## Pre-req for demo
### 1. open-cluster-management hub
place kubeconfig in `contrib/demo/kubeconfig` as `hub.kubeconfig`

Install Red Hat Advanced Cluster Management from Operator Hub

### 2. at least 2 kubernetes cluster
place the seperate kubeconfig files for the cluster in `contrib/demo/kubeconfig/managedclusters`

#### Note on creating kubeconfig's
  1. `export KUBECONFIG=./kubeconfig/hub.kubeconfig`
  2. Connect to the hub cluster using `oc login`, this will create a valid kubeconfig.
  3. Repeat steps 1 & 2 using `export KUBECONFIG=./kubeconfig/managedclusters/kubeconfig0X` where X is incremented for each cluster. (Any file name will be picked up by the scripts)

## Setup the demo
```
./demo-setup.sh
```

this script will first compile `kcp` and `kcp-ocm` as well as download `cm-cli` for open-cluster-management

the script will than wait for user key press to start both `kcp` and `kcp-ocm`
`kcp` and `kcp-ocm` will be left running till another user key press is recieved 

leave this script running while running the demo than stop the script by pressing any key

## Running the demo
```
./demo -n
```
the demo will wait for key press to proceed after each section 

## Demo
1. A connection to the hub is validated, along with the install of ACM
2. It is shown that no clusters are currently imported
3. Using the provided kubeconfig's, clusters are imported
4. We show that the kcp is enabled and the deployment.app CRD is applied
5. A deployment.app resource is created in kcp
6. This causes the kcp-ocm controller to create a Placement Rule, which is shown, as well as its decision contents (targets)
7. Then the ManifestWork created to target the clusters determined by placement
8. Finally the remote clusters are queried to see that the deployment.app created in kcp is applied to the remote clusters
