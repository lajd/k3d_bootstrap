# https://k3d.io/v5.4.6/usage/advanced/cuda/ 

K3S_VERSION := v1.26.1-k3s1
CLUSTER_NAME := cpu-cluster

install-k3d:
	wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

create-cluster:
	sudo k3d cluster create ${CLUSTER_NAME} --image=rancher/k3s:${K3S_VERSION}

delete-cluster:
	k3d cluster delete ${CLUSTER_NAME}

configure-kubectl:
	$(eval KUBECONFIG := $(shell k3d kubeconfig write ${CLUSTER_NAME}))
	echo "KUBECONFIG=$(KUBECONFIG)" >> ~/.profile
	echo "Run the following command in your shell:"
	echo "export KUBECONFIG=$(KUBECONFIG) "

list-clusters:
	k3d cluster list
