# 安装

## 在集群中创建 flux-system Kustomization

创建集群1: my-cluster

```bash
flux bootstrap git \
  --url=https://github.com/sznrit/fluxcd.git \
  --branch=main \
  --path=./clusters/my-cluster \
  --username=sznrit \
  --password= \
  --token-auth=true
```

## 集群中的 Kustomization 资源
```bash
# 强制 Flux 立即拉取 Git 仓库
flux reconcile source git flux-system -n flux-system

# 强制 Flux 立即应用 Kustomization
flux reconcile kustomization flux-system -n flux-system

# flux-system（由 bootstrap 自动创建）
kubectl get kustomization flux-system -n flux-system
```

## 删除集群中的 Kustomization 资源
```bash
# 删除旧的 Kustomization
kubectl delete kustomization flux-system -n flux-system

# 删除旧的 GitRepository
kubectl delete gitrepository flux-system -n flux-system
```