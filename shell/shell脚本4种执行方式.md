## shell脚本的4种执行方式

> shell脚本通常的执行方式有四种：工作目录执行，绝对路径执行，sh执行，shell环境执行

### 工作目录执行

```shell
# 直接在当前目录执行脚本
./myshell.sh
```

### 绝对路径执行

```shell
# 使用完整的绝对路径执行脚本
/home/username/myshell.sh
```

### sh执行

```shell
# 使用指定的bash或者sh执行脚本
bash myshell.sh
sh myshell.sh
```

### shell环境执行

```shell
# 在当前使用的shell环境中执行。使用. 或者source接脚本
. myshell.sh
source myshell.sh
```