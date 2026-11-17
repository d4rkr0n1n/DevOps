# Multi-Node kind Cluster

A local Kubernetes cluster with 1 control-plane and 3 worker nodes (`control-plane-1`, `worker-1`, `worker-2`, `worker-3`), defined in [`kind-config.yml`](kind-config.yml).

Run all commands from this directory.

## Create the cluster

```powershell
kind create cluster --name kind --config .\kind-config.yml
kubectl cluster-info --context kind-kind
```

## Label worker nodes

kind doesn't assign a role label to workers, so `kubectl get nodes` shows `<none>` for them. Label them:

```powershell
kubectl label node worker-1 node-role.kubernetes.io/worker=worker
kubectl label node worker-2 node-role.kubernetes.io/worker=worker
kubectl label node worker-3 node-role.kubernetes.io/worker=worker
```

Verify:

```powershell
kubectl get nodes
```

## Recreate the cluster

```powershell
kind delete cluster --name kind
kind create cluster --name kind --config .\kind-config.yml
```

## Delete the cluster

```powershell
kind delete cluster --name kind
```
