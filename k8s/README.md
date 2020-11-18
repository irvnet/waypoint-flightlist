# Kubernetes

## The Plan

- Use and set up https://kind.sigs.k8s.io/ locally
  + Follow the quick start guide to get more familiar with kind
  + https://kind.sigs.k8s.io/docs/user/quick-start/

## Requirements

- Docker installed locally
- Golang 1.11+ installed locally
- kubectl installed and available on the path
  + https://kubernetes.io/docs/tasks/tools/install-kubectl/
- A way to automate and setup a realistic but minimalist environment to test Waypoint with

### Linux Steps

TODO: Turn this into a script, and automate grabbing local docker subnet and placing it into metallb config

1) kind create cluster --config cluster-config.yaml
2) kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/namespace.yaml
3) kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
4) kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.3/manifests/metallb.yaml
5) Get docker subnet, and update metallb values to represent your local docker subnet
5) kubectl apply -f metallb-config.yaml