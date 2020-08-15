# Cheatsheet

## 分割文件

若要将一个数千行的 JSON Lines 文件（`new_labeling_tasks.jl`）分割为 1000 行的子文件，可使用如下命令：

```shell script
split -l 1000 -d --additional-suffix=.jl new_labeling_tasks.jl new_labeling_tasks_
```

这将会生成 `new_labeling_tasks_00.jl`、`new_labeling_tasks_01.jl`、... 、等。

## 统计文件行数

```shell script
wc -l new_labeling_tasks.jl
```

示例输出：`9096 new_labeling_tasks.jl`

## 生成随机字符串

```shell script
tr -dc a-zA-Z0-9 < /dev/urandom | head -c 50
```

示例输出：`viYAYCs3uFHa0hE3oRRaDkv476dR5AYH6MXUPGhUQPZAAMp82h`

## base64 编码/解码

编码：

```shell script
echo yintrust | base64
```

示例输出：`eWludHJ1c3QK`

解码：

```shell script
echo eWludHJ1c3QK | base64 -d
```

示例输出：`yintrust`

## md5 哈希

```shell script
echo -n yintrust | md5sum | cut -d ' ' -f 1
```

示例输出：`a6ade2856ca8717c1643aead34c96088`
