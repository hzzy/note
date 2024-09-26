# centos man命令

manual 的缩写 使用手册的意思

没有 memcpy 的手册页条目
执行以下命令
```
yum install -y man man-pages man-pages-overrides
```

```
sudo mandb 更新man的数据库 同步成最新
```

# 分类

1. 可执行程序或命令的手册
2. 系统调用的手册
3. 库调用的手册
4. 文件 （/etc/passwd）
5. 等等


# 使用
* man 数字 命令/函数 可以查到相关的命令和函数 数字是编号
* 不加数字 默认从较小的手册中寻找命令和函数

# 数字
* 数字1‌代表‌可执行程序或shell命令‌
* 数字2‌代表‌系统调用（由内核提供的函数）
* 数字3‌代表‌库函数（程序库中的函数）‌
* 数字4‌代表‌特殊文件（通常位于/dev目录中）‌
* 数字5‌代表‌文件格式和约定‌，例如/etc/passwd
* 数字6‌代表‌游戏‌
* 数字7‌代表‌杂项（包括宏包和约定）‌
* ‌数字8‌代表‌系统管理命令（通常仅适用于root）‌

# 手册页的不同区域
分区域展示 大些 粗体 靠左展示
```
NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about  the FILEs (the current directory by default).
       Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci‐
       fied.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.

       -a, --all
              do not ignore entries starting with .
      ......
      
AUTHOR
       Written by Richard M. Stallman and David MacKenzie.

COPYRIGHT
       Copyright © 2013 Free Software Foundation, Inc.   License  GPLv3+:  GNU
       GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       The full documentation for ls is maintained as a  Texinfo  manual.   If
       the  info and ls programs are properly installed at your site, the com‐
       mand

              info coreutils 'ls invocation'

       should give you access to the complete manual.
```
* NAME 名字 + 简单描述
* SYNOPSIS 摘要 显示了所有可能的参数组合 [option] 表示可选参数 粗体表示原封不动的输入 下划线的文字表示用实际内容替换
* DESCRIPTION 详细描述
* AUTHOR 作者
* COPYRIGHT 版权
* SEE ALSO 另见

# 查找命令
apropos + 关键字
根据手册中的关键字来查找命令

# 其他查看手册命令
命令 -h 参数 显示帮助文档
whatis man命令精简版本 



