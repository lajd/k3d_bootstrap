# Create CPU and GPU K3d clusters

## CPU

Optionally change the Makefile variables at `k3d/cpu/Makefile`.

```
K3S_VERSION := v1.26.1-k3s1
CLUSTER_NAME := cpu-cluster
```

Create a CPU cluster:
```
cd cpu
create-cluster

make configure-kubectl

# Export the KUBECONFIG envar in your shell
export KUBECONFIG=$HOME/.k3d/kubeconfig-cpu-cluster.yaml 

kubectl get pods -A

```

## GPU


You must change the variable `IMAGE_REGISTRY`, and optionally other Makefile variables at `k3d/gpu/Makefile`.

```
K3S_VERSION := v1.26.1-k3s1
IMAGE_REGISTRY := TODO
CLUSTER_NAME := gpu-cluster
```

```
cd gpu

make build

create-cluster

make configure-kubectl

# Export the KUBECONFIG envar in your shell
export KUBECONFIG=$HOME/.k3d/kubeconfig-gpu-cluster.yaml 

kubectl get pods -A

make deploy-test-pod 
```