

# 命令使用

记录一些比较有用的命令的使用方式，或者一些常用操作如何实现。

### 删除软连接

```
# delete directly
rm link_1 link_2

# unlink, accepts only a single argument.
# 同样会删除文件
unlink symlink_name


# Find and Delete Broken Symbolic Links. maxdepth can pass subdirectories
find /path/to/directory -xtype l
find /path/to/directory -maxdepth 1 -xtype l
find /path/to/directory -xtype l -delete
```

