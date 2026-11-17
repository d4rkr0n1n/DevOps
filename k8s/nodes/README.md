# Inspecting Nodes

Commands for looking at the nodes of a running cluster. The examples use the node names from the [multi-node kind cluster](../multi-node/README.md) (`control-plane-1`, `worker-1`, `worker-2`, `worker-3`), so create that cluster first.

## List nodes with extra details

```powershell
kubectl get nodes -o wide
```

Adds columns to the default output: internal/external IP, OS image, kernel version, and container runtime.

## Show node labels

```powershell
kubectl get nodes --show-labels
```

Lists every label on each node, such as `kubernetes.io/hostname`, `kubernetes.io/os`, and the `node-role.kubernetes.io/*` role labels. Use it to check that the worker role labels were applied.

## Describe a node

```powershell
kubectl describe node worker-1
```

A readable summary of a single node: labels, taints, conditions (`Ready`, `MemoryPressure`, `DiskPressure`, ...), capacity and allocatable resources, the pods running on it with their resource requests and limits, and recent events. Start here when a node is `NotReady` or pods won't schedule on it.

## Get the full node object

```powershell
kubectl get node worker-1 -o yaml
```

Prints the complete Node object as the API server stores it: `metadata` (labels, annotations), `spec` (pod CIDR, taints), and `status` (addresses, conditions, capacity, node info). Use `-o json` instead if you want to pipe it to a tool such as `jq`.
