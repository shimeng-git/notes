# awk

`awk`是一个文本处理程序，依次处理每行文件，并读取里面的每一个字段。

## 基本介绍

```shell
# 格式
$ awk 动作 文件名

# 示例
$ awk '{print $0}' demo.txt
$ echo 'this is a test' | awk '{print $0}'

awk默认分隔符是空格或者制表符，使用-F可以指定制表符
awk -F ':' '{ print $1 }' demo.txt

print命令里面的逗号，表示输出的时候，两个部分之间使用空格分隔。
awk -F ':' '{print $1, $(NF-1)}' demo.txt
# output: root /root

# 使用双引号原样输出字符
awk -F ':' '{print NR ") " $1}' demo.txt
```

| 变量        | 字段                                             |
| ----------- | ------------------------------------------------ |
| $0          | 当前行                                           |
| $1 -- $n    | 当前行的各个列                                   |
| NF  ->  $NF | 当前行列的数量 --> 最后一列                      |
| FILENAME    | 当前文件名                                       |
| FS          | 字段分隔符，默认空格和制表符                     |
| RS          | 行分隔符，默认是换行符                           |
| OFS         | 输出字段的分隔符，用于打印时的分隔字段，默认空格 |
| ORS         | 输出记录的分隔符，用于打印时的分隔记录，默认换行 |
| OFMT        | 输出格式，默认`%.6g`                             |



| 函数                      | 作用              |
| ------------------------- | ----------------- |
| toupper()/tolower()       | 字符转换为大/小写 |
| length()                  | 返回字符长度      |
| sunstr()                  | 返回子字符串      |
| sin()/cos()/sqrt()/rand() | 数学计算          |

## 条件

`awk`可以指定条件，从而只输出符合条件的行。输出条件写在动作前面：

```shell
awk 'condition action' filename

# 输出包含usr的行（正则）
awk -F ':' '/usr/ {print $1}' demo.txt

# 输出奇数行
awk -F ':' 'NR % 2 == 1 {print $1}' demo.txt

# 输出第一个字段等于给定值的行
$ awk -F ':' '$1 == "root" {print $1}' demo.txt
$ awk -F ':' '$1 == "root" || $1 == "bin" {print $1}' demo.txt


```

对于复杂的条件，可以使用`if`语句编写。

```bash
# 输出
awk -F ':' '{if ($1 > "m") print $1}' demo.txt
awk -F ':' '{if ($1 > "m") print $1; else print "---"}' demo.txt
```

















