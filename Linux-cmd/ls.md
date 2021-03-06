# ls
显示指定工作目录下的内容及属性信息。


### 语法
```
ls [选项] [文件]
```

### 常用参数
* -a : 显示所有文件及目录 (包括以“.”开头的隐藏文件)
* -l : 使用长格式列出文件及目录信息
* -r : 将文件以相反次序显示(默认依英文字母次序)
* -t : 根据最后的修改时间排序
* -A : 同 -a ，但不列出 “.” (当前目录) 及 “..” (父目录)
* -S : 根据文件大小排序
* -R : 递归列出所有子目录
* -F : 在列出的文件名称后加一符号；例如可执行档则加 "*", 目录则加 "/"


### sample
```
# 列出当前目录下所有以f开头的文件以及其子目录，并根据最后修改时间排序
ls -ltr f*
# 列出当前目录下所有文件，并在目录名后加 / ，在可执行文档后加 *
ls -AF
```




