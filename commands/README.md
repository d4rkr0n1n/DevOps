# Toolchain Setup (Windows)

Install the local Kubernetes toolchain with [Chocolatey](https://chocolatey.org/). Run from an elevated (Administrator) shell.

## Docker Desktop

```powershell
choco install docker-desktop -n -y
```

## kubectl

```powershell
choco install kubernetes-cli -y
```

## kind

```powershell
choco install kind -y
```
