# 🕹️ Slim playground for OpenNMS Horizon in Kubernetes

This is a repository to learn how to run OpenNMS components in Kubernetes.
To spent not too much time with what flavour of Kubernetes we are going to deal with, I use [kind](https://kind.sigs.k8s.io/) to get it going as quick as possible.

## 💅 Requirements

* At least 8G RAM
* Docker or Podman
* [Kind](https://kind.sigs.k8s.io/)
* Kubectl installed
* [Kustomize](https://kustomize.io/)
* Helm 3 to install PostgreSQL (optional)
* The configuration for Horizon is maintained in Git and uses a [git-container](https://github.com/labmonkeys-space/app-container/tree/main/git) as an init.

The instructions below will deploy everything in the namespace "default".

## 👩‍🔧 Usage

### Create a local Kubernetes Cluster

```shell
kind create cluster
```

When you manage multiple cluster from your computer, the context is set to your newly created kind cluster.
You can verify your context with

```shell
kubectl config get-contexts
```

### Install PostgreSQL database

💁‍♀️ OpenNMS Horizon as today, supports only up to PostgreSQL 15.
I've found only 14 and 17+ images in the Bitnami PostgreSQL charts and set it the latest major version 14.

```shell
helm install onms-postgres oci://registry-1.docker.io/bitnamicharts/postgresql --set "image.tag=14"
```

### Deploy OpenNMS Horizon

```shell
cd kustomize
kustomize build | kubectl apply -f -
```
