# Docker 与 K8s

## 批量删除驱逐（Evicted）的 Pod

```sh
kubectl get pod -n test | grep Evicted | awk '{print $1}' | xargs kubectl delete -n test pod
```

## 删除孤儿（Orphaned）Pod

1. 先查出 Hash：
   ```sh
   tail -n 10 /var/log/syslog | grep Orphaned | awk '{print$12}' | sed 's/"//g' | uniq
   ```
   示例输出：`0b0b9b99-6a28-11ec-a6aa-002278b0b72f`
3. 再根据 Hash 删除相关目录：
   ```sh
   rm -rf /var/lib/kubelet/pods/0b0b9b99-6a28-11ec-a6aa-002278b0b72f
   ```
