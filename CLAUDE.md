# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A DevOps playground repo with no application code: there's nothing to build, lint, or test. It holds a local Kubernetes setup (kind), tool install notes, and a placeholder GitHub Actions workflow. Development happens on Windows (Chocolatey, PowerShell-style paths).

## Layout

- `commands/README.md`: Chocolatey commands to install the toolchain (`docker-desktop`, `kubernetes-cli`, `kind`).
- `k8s/multi-node/`: a 4-node kind cluster (1 control-plane, 3 workers). `kind-config.yml` uses `kubeadmConfigPatches` to give nodes fixed names (`control-plane-1`, `worker-1`..`worker-3`) so later `kubectl` commands can refer to them by name.
- `k8s/nodes/README.md`: `kubectl` commands for inspecting nodes (`get -o wide`, `--show-labels`, `describe`, `-o yaml`), using the multi-node cluster's node names.
- `k8s/plans/`: learning roadmap notes (e.g. upcoming topics like node maintenance and taints/tolerations).
- `.github/workflows/blank.yml`: CI on push/PR to `main` plus manual dispatch. The `build` job (echo placeholders) is followed by `dev-deployment`, which `needs: build` and targets the `dev` GitHub environment.

## Local cluster commands

Run these from `k8s/multi-node/`:

```powershell
kind create cluster --name kind --config .\kind-config.yml
kubectl cluster-info --context kind-kind

# kind doesn't set worker role labels; add them so `kubectl get nodes` shows the role
kubectl label node worker-1 node-role.kubernetes.io/worker=worker
kubectl label node worker-2 node-role.kubernetes.io/worker=worker
kubectl label node worker-3 node-role.kubernetes.io/worker=worker
kubectl get nodes

kind delete cluster --name kind
```

The label commands depend on the node names set in `kind-config.yml`. If you rename nodes there, update them in `k8s/multi-node/README.md` and `k8s/nodes/README.md` too.
