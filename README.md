# Cheatsheet

- [Hotkey](hotkey.md)

## 分割文件

若要将一个数千行的 JSON Lines 文件（`new_labeling_tasks.jl`）分割为 1000 行的子文件，可使用如下命令：

```shell
split -l 1000 -d --additional-suffix=.jl new_labeling_tasks.jl new_labeling_tasks_
```

这将会生成 `new_labeling_tasks_00.jl`、`new_labeling_tasks_01.jl`、... 、等。

## 合并文件

若要将两个文件合并成一个文件，可使用如下命令：

```shell
cat a.txt b.txt > all.txt
```

这将会生成 `all.txt` 文件。

## 统计文件行数

```shell
wc -l new_labeling_tasks.jl
```

示例输出：`9096 new_labeling_tasks.jl`

## 生成随机字符串

```shell
tr -dc a-zA-Z0-9 < /dev/urandom | head -c 50
```

示例输出：`viYAYCs3uFHa0hE3oRRaDkv476dR5AYH6MXUPGhUQPZAAMp82h`

## base64 编码/解码

编码：

```shell
echo yintrust | base64
```

示例输出：`eWludHJ1c3QK`

解码：

```shell
echo eWludHJ1c3QK | base64 -d
```

示例输出：`yintrust`

## md5/sha1 哈希

```shell
echo -n yintrust | md5sum | cut -d ' ' -f 1
# or
echo -n yintrust | sha1sum | cut -d ' ' -f 1
```

示例输出：

- `a6ade2856ca8717c1643aead34c96088`
- `73171da61cd9f77537128cf38c84ecf7eda3d95d`

## 统计最常用的 20 个命令

下述命令引用自 Oh My Zsh 的 [`zsh_stats`](https://github.com/ohmyzsh/ohmyzsh/blob/master/lib/functions.zsh#L1-L3) 命令

```shell
fc -l 1 | awk '{CMD[$2]++;count++;}END { for (a in CMD)print CMD[a] " " CMD[a]/count*100 "% " a;}' | grep -v "./" | column -c3 -s " " -t | sort -nr | nl |  head -n20
```

示例输出：

```text
     1	1466  14.5437%     ls
     2	1425  14.1369%     git
     3	1081  10.7242%     docker-compose
     4	960   9.52381%     cd
     5	811   8.04563%     sudo
     6	283   2.80754%     rm
     7	266   2.63889%     ssh
     8	211   2.09325%     cat
     9	188   1.86508%     docker
    10	180   1.78571%     mv
    11	170   1.68651%     subl
    12	170   1.68651%     python3
    13	160   1.5873%      curl
    14	122   1.21032%     touch
    15	108   1.07143%     history
    16	101   1.00198%     proxychains4
    17	101   1.00198%     mkdir
    18	92    0.912698%    pip
    19	76    0.753968%    pip3
    20	73    0.724206%    vagrant

```

## 使用 `ffmpeg` 将多个 `.ts` 文件合并为单个 mp4 文件

```shell
cat segment_1.ts segment_2.ts segment_3.ts > all.txt
ffmpeg -f concat -safe 0 -i all.txt -c copy all.mp4
```
