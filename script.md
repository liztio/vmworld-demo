## Setup `kind`

```shell
kind create cluster --config ./kind-cluster-with-extramounts.yaml --name vmworld-manager
export KUBECONFIG="$(kind get kubeconfig-path --name="vmworld-manager")"
```

## install the infrastructure providers


```
kubectl create -f https://github.com/kubernetes-sigs/cluster-api/releases/download/v0.2.7/cluster-api-components.yaml
kubectl create -f https://github.com/kubernetes-sigs/cluster-api-bootstrap-provider-kubeadm/releases/download/v0.1.5/bootstrap-components.yaml
kubectl create -f https://github.com/kubernetes-sigs/cluster-api-provider-docker/releases/download/v0.2.1/provider-components.yaml
```

## Setup Cluster

```
kubectl apply -f cluster.yaml
kubectl apply -f docker-cluster.yaml
```

## Setup Control Plane
```
kubectl apply -f control-plane.yaml
kubectl apply -f docker-control-plane.yaml 
kubectl apply -f kubeadm-control-plane.yaml
```

## Get the secret

```
kubectl get secret capi-quickstart-kubeconfig -o json | jq -r '.data.value' | base64 -d > cluster.kubeconfig
```

## Make some machines

```
kubectl apply -f machine-deployment.yaml
kubectl apply -f docker-machine-deployment.yaml 
kubectl apply -f kubeadm-machine-deployment.yaml
```

## See the nodes!

```
```
