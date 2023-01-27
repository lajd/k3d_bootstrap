# https://k3d.io/v5.4.6/usage/advanced/cuda/ 
# See https://github.com/k3d-io/k3d/issues/1108 for helpful support

K3S_VERSION := v1.26.1-k3s1
IMAGE_REGISTRY := TODO
CLUSTER_NAME := gpu-cluster


install-k3d:
	wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

build:
	IMAGE_REGISTRY=${IMAGE_REGISTRY} K3S_TAG=${K3S_VERSION} bash build.sh

create-cluster:
	sudo k3d cluster create ${CLUSTER_NAME} --image=${IMAGE_REGISTRY}/rancher/k3s:${K3S_VERSION}-cuda --gpus=all

delete-cluster:
	k3d cluster delete ${CLUSTER_NAME}

configure-kubectl:
	$(eval KUBECONFIG := $(shell k3d kubeconfig write ${CLUSTER_NAME}))
	echo "KUBECONFIG=$(KUBECONFIG)" >> ~/.profile
	echo "Run the following command in your shell:"
	echo "export KUBECONFIG=$(KUBECONFIG) "

list-clusters:
	k3d cluster list

deploy-test-pod:
	kubectl apply -f cuda-vector-add.yaml
	kubectl wait --for=condition=ready pod/cuda-vector-add
	kubectl logs cuda-vector-add
