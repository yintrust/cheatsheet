# Docker 与 K8s

## 获取 Docker Registry 上的所有 image

```sh
curl https://<ip>:<port>/v2/_catalog | python3 -m json.tool
```

示例输出：

```sh
{
    "repositories": [
        "yintrust-web",
        ...
    ]
}
```

## 获取 Docker Registry 上指定的 image 的所有 tag

```sh
curl https://<ip>:<port>/v2/yintrust-web/tags/list | python3 -m json.tool
```

示例输出：

```sh
{
    "name": "yintrust-web",
    "tags": [
        "201907122041",
        "201906071308",
        ...
    ]
}
```

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
