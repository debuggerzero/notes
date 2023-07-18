# Linux

## 文件系统

1. **文件结构**
   - /			     -- 根目录
     - bin     -- 存放可执行文件命令
     - etc      -- 存放配置文件
     - var      -- 存放日志文件
     - lib       -- 存放安装包 & 头文件
     - home -- 所有用户的家目录
     - proc   -- 存放计算机信息
   
2. **绝对路径**
  
   - /home/zero/main.cpp
   
3. **相对路径**
   - zero/main.cpp
   
4. **其他路径**

   - `.`  当前目录
     
- `..` 上级目录
  
   - `~` 家目录

5. **常用指令**
  
    1. `ctrl c` 

       - 杀死某个进程

       - 换行`ctrl u` 清空行

    2. `tab` 补全命令

    3. `ls`
       - 显示文件列表
       - `-l` 显示文件详细信息
       - `-a` 显示所有文件
    4. `pwd` 显示当前路径
    5. `cd x` 进入目录 x
    6. `cp x y` 
         - 将 x 复制到 y
    
         - `-r` 将 x 目录中的所有文件复制到 y 
    7. `mkdir x`  创建目录 x
    8. `touch x` 创建文件 x
    9. `rm x`
           - 删除文件 x
           - `-r` 删除文件夹
    10. `mv x y` 将 x 移动到 y
    11. `cat x` 查看 x 内容

## Tmux	

1. **功能**
   1. 分屏
   2. 运行断开 Terminal 连接后，继续运行进程
2. **常用指令**
   1. `tmux` 新建一个 session
   2. `tmux a` 打开之前挂起的 session

## Vim

1. **功能**
   1. 命令行模式下文本编辑器
   2. 根据文件扩展名自动自动辨别编程语言。支持代码缩进、代码高亮等功能
   3. 使用方式：`vim filename`
   
2. **模式**
   1. 一般命令模式
   2. 编辑模式
   3. 命令行模式
   
3. **操作**
   1. `i` 进入编辑模式
   2. `esc` 进入一般命令模式
   3. `h` 光标向左移动一个字符
   4. `j` 光标向下移动一个字符
   5. `k` 光标向上移动一个字符
   6. `l` 光标向右移动一个字符
   7. `n<space>` 光标向右移动这一行的 n 个字符
   8. `0` 或 `[Home]`光标移动到本行开头
   9. `$` 或 `[End]`光标移动到本行末尾
   10. `G` 光标移动到最后一行
   11. `n` 或 `nG`：n 为数字，光标移动到第 n 行
   12. `gg` 光标移动到第一行，相当于 1 G
   13. `n<Enter>` n 为数字，光标向下移动 n 行
   14. `/word` 向光标之下寻找第一个值为 word 的字符串。
   15. `? word`向光标之上寻找第一个值为 word 的字符串。
   16. `n` 重复前一个查找操作
   17. `N` 反向重复前一个查找操作
   18. `:n1,n2s/word1/word2/g` n1与 n2 为数字，在第 n1 行与 n2 行之间寻找 word1 这个字符串，并将该字符串替换为 word2
   19. `:1,$s/word1/word2/g` 将全文的 word1 替换为 word2
   20. `:1,$s/word1/word2/gc` 将全文的 word1 替换为 word2，且在替换前要求用户确认。
   21. `v` 选中文本
   22. `d` 删除选中的文本
   23. `dd` 删除当前行
   24. `y` 复制选中文本
   25. `yy` 复制当前行
   26. `p` 将复制的数据在光标的下一行 / 下一个位置粘贴
   27. `u` 撤销
   28. `ctrl + r` 取消撤销
   29. `>` 将选中的文本整体向右缩进
   30. `<` 将选中的文本整体向左缩进一次
   31. `:w` 保存
   32. `:w!` 强制保存
   33. `:q` 退出
   34. `:q!` 强制退出
   35. `:wq` 保存并退出
   36. `:set paste` 设置成粘贴模式，取消代码自动缩进
   37. `:set nopaste` 取消粘贴模式，开启代码自动缩进
   38. `:set nu` 显示行号
   39. `:set nonu` 隐藏行号
   40. `gg=G` 将全文代码格式化
   41. `:noh` 关闭查找关键词高亮
   42. `ctrl + q` 当vim卡死时，可以取消当前正在执行的命令
   
## Shell 

   1. **概论**

      shell 是我们通过命令行与操作系统沟通的语言。

      shell 脚本可以直接在命令行中执行，也可以将一套逻辑组织成一个文件，方便复用。

      `chmod +x xx.sh` 给 xx 文件添加权限

   2. **注释**

      1. 单行注释

      ```shell
      # 这是一行注释
      
      echo "hello world" # 这也是注释
      ```

      2. 多行注释

      ```shell
      :<<EOF
      第一行注释
      第二行注释
      第三行注释
      EOF
      ```

   3. **变量**

      1. 定义变量

      ```shell
      name1='hwc'
      name2="hwc"
      name3=hwc
      ```

      2. 使用变量

      `${name}`

      ```shell
      name=hwc
      echo $name # 输出 hwc
      echo ${name} # 输出 hwc
      echo ${name}!!! # 输出 hwc!!!
      ```

      3. 只读变量

      `readonly` 或 `declare`

      ```shell
      name=hwc
      readonly name
      declare -r name
      ```

      4. 删除变量

      `unset`

      ```shell
      name=hwc
      unset name
      echo $name
      ```

      5. 变量类型

         1. 自定义变量

            子进程不能访问的变量

         2. 环境变量

            子进程可以访问的变量

         自定义变量改成环境变量

         ```shell
         name=hwc
         export name
         declare -x name
         ```

         环境变量改为自定义变量

         ```shell
         export name=hwc
         declare +x name
         ```

      6. 字符串

         1. 单引号与双引号的区别

            - 单引号中的内容会原样输出，不会执行、不会取变量

            - 双引号中的内容可以执行、可以取变量

         2. 获取字符串的长度

         ```shell
         name="hwc"
         echo ${#name} # 输出3
         ```

         3. 提取子串

         ```shell
         name="hello, hwc"
         echo ${name:0:5} # 提取从0开始的5个字符
         ```

   4. **默认变量**

      ```shell
      #! /bin/bash
      
      echo "文件名:"$0
      echo "第一个参数:"$1
      echo "第二个参数:"$2
      ```

      | 参数        | 说明                                                         |
      | ----------- | ------------------------------------------------------------ |
      | $#          | 代表文件传入的参数个数，如上例中值为4                        |
      | $*          | 由所有参数构成的用空格隔开的字符串，如上例中值为"$1 $2 $3 $4" |
      | $@          | 每个参数分别用双引号括起来的字符串，如上例中值为"$1" "$2" "$3" "$4" |
      | $$          | 脚本当前运行的进程ID                                         |
      | $?          | 上一条命令的退出状态（注意不是stdout，而是exit code）。0表示正常退出，其他值表示错误 |
      | $(command)  | 返回 command 这条命令的 stdout（可嵌套）                     |
      | \`command\` | 返回 command 这条命令的 stdout（不可嵌套）                   |

   5. **数组**

      1. 定义用小括号表示，元素之间用空格隔开

          ```shell
          array=(1 abc "def" hwc)
          array[0]=1
          array[1]=abc
          array[2]="def"
          array[3]=hwc
          ```

      2. 读取

          ```shell
          ${array[index]} # 读取数组某个值
          ${array[@]} # 读取整个数组
          ${array[*]} # 读取整个数组
          ${#array[@]} # 读取数组长度
          ${#array[*]} # 读取数组长度
          ```

   6. `expr` **命令**

      ```shel
      expr 表达式
      ```

      - 表达式说明:

        - 用空格隔开每一项。
        - 用反斜杠放在 shell 特定的字符前面。
        - 对包含空格和其他特殊字符的字符串要用引号括起来。
        - `expr` 会在 `stdout` 中输出结果。

      - 字符串表达式

        - `length STRING` 返回 `STRING` 的长度。

        - `index STRING CHARSET`

          `CHARSET` 中任意单个字符在 `STRING` 中最前面的字符位置，下标从 1 开始。

          如果在 `STRING` 中完全不存在 `CHARSET` 中的字符，则返回 。

        - `substr STRING POSITION LENGTH`

          返回 `STRING` 字符串中从 `POSITION` 开始，长度最大为 `LENGTH` 的子串。如果 `POSITION` 或 `LENGTH` 为负数， 0 或非数值，则返回空字符串。

      - 整数表达式

        - `expr` 支持普通的算术操作，算术表达式优先级低于字符串表达式，高于逻辑关系表达式。
          - `+ -` 加减运算。两段参数会转换为整数，如果转换失败则报错。
          - `* / %` 乘，除，取模运算。两段参数会转换为整数，如果转换失败则报错。
          - `()` 可以改变优先级，但需要用反斜杠转义。

      - 逻辑关系表达式

        - `|` 如果第一个参数非空且非 0，则返回第一个参数的值，否则返回第二个参数的值，但要求第二个参数的值也是非空或非 0，否则返回 0。如果第一个参数是非空或非 0 时，不会计算第二个参数。
        - `&` 如果两个参数都非空且非 0，则返回第一个参数，否则返回 0。如果第一个参为 0 或为空，则不会计算第二个参数。
        - `< <= = == != >= >` 比较两端的参数，如果为 true，则返回 1，否则返回 0。”==” 是 ”=” 的同义词。”expr” 首先尝试将两端参数转换为整数，并做算术比较，如果转换失败，则按字符集排序规则做字符比较。
        - `()` 可以改变优先级，但需要用反斜杠转义。

   7. `read` 命令用于从标准输入中读取单行数据

      参数说明

      - `-p` 后面可以接提示信息
      - `-t` 后面跟秒数，定义输入字符的等待时间，超过等待时间后会自动忽略此命令

   8. `echo` 用于输出字符串。

   9. `printf` 命令用于格式化输出，默认不会在字符串末尾添加换行符

## ssh

1. **基本用法**

    ```shell
    ssh user@hostname
    ```

- `user`: 用户名
- `hostname`: IP地址或域名

默认端口号为 22，如果想登录某一特定端口：

    ```shell
    ssh user@hostname -p 22
    ```

2. **配置文件**

    ```shell
    # ~/.ssh/config
    Host aliyun
        HostName ip
        User 用户名
    ```

3. **密钥登陆**

- 创建密钥

    ```shell
    ssh-keygen
    ```

- ~/.ssh/ 目录下会多两个文件：
  - `id_rsa` ：密钥
  - `id_rsa.pub`：公钥
- 将公钥内容，复制到服务器中的 `~/.ssh/authorized_keys` 文件里即可
- 也可以通过命令：

    ```shell
    ssh-copy-id ...
    ```

4. scp 传文件

- **基本用法**

    ```shell
    # 将 source 路径下的文件复制到 destination 中
    scp source destination
    
    # 一次复制多个文件
    scp source1 source2 destination
    
    # 将本地家目录中的 tmp 文件夹复制到 myserver 服务器中的 /home/acs/ 目录下
    scp -r ~/tmp myserver:/home/acs/
    
    # 将本地家目录中的 tmp 文件夹复制到 myserver 服务器中的 ~/homework/ 目录下
    scp -r ~/tmp myserver:homework/
    
    # 将 myserver 服务器中的 ~/homework/ 文件夹复制到本地的当前路径下。
    scp -r myserver:homework .
    
    # 使用scp配置其他服务器的vim和tmux
    scp ~/.vimrc ~/.tmux.conf myserver:
    ```

## 管道、环境变量与常用指令

### 管道

- **管道概念**
  - 管道类似于文件重定向，可以将前一个命令的 `stdout` 重定向到下一个命令的 `stdin`。
- **要点**
  1. 管道命令仅处理 `stdout` ，会忽略 `stderr`。
  2. 管道右边的命令必须能接受 `stdin`。
  3. 多个管道命令可以串联。
- **与文件重定向的区别**
  - 文件重定向左边为命令，右边为文件。
  - 管道左右两边均为命令，左边有 `stdout`，右边有 `stdin`。

### 环境变量

- **概念**
  - Linux 系统中会用很多环境变量来记录配置信息。
  - 环境变量类似于全局变量，可以被各个进程访问到。我们可以通过修改环境变量来方便的修改系统配置。
- **查看**
  
  - 列出当前环境下的所有环境变量：
    ```shell
    env # 显示当前用户的变量
    set # 显示当前 shell 的变量，包括当前用户的变量
    export # 显示当前导出用户变量的 shell 变量
    ```
    
  - 输出某个环境变量的值
  
    ```shell
    echo $PATH
    ```
  
- **修改**

  为了将对环境变量修改应用到未来所有环境下，可以将修改命令放到`~/.bashrc` 文件中。

  修改完 `~/.bashrc` 文件后，记得执行 `source ~/.bashrc` ，来将修改应用到当前的 `bash` 环境下。

### 常用命令

#### 系统状况

1. `top`：查看所有进程的信息（Linux 的任务管理器）
   - 打开后，输入 `M`：按使用内存排序

   - 打开后，输入 `P`：按使用 CPU 排序

   - 打开后，输入 `q`：退出

2. `df -h`：查看硬盘使用情况
3. `free -h`：查看内存使用情况
4. `du -sh`：查看当前目录占用的硬盘空间
5. `ps aux`：查看所有进程
6. `kill -9 pid`：杀死编号为  `pid` 的进程
   - 传递某个具体的信号：`kill -s SIGTERM pid`
7. `netstat -nt`：查看所有网络连接
8. `w`：列出当前登陆的用户
9. `ping www.baidu.com`：检查是否连网

#### 文件权限

1. `chmod`：修改文件权限
   - `chmod +x xxx`：给xxx添加可执行权限
   - `chmod -x xxx`：去掉xxx的可执行权限
   - `chmod 777 xxx`：将xxx的权限改成777
   - `chmod 777 xxx -R`：递归修改整个文件夹的权限

#### 文件检索

1. `find /path/to/directory/ -name '*.py'`：搜索某个文件路径下的所有`*.py` 文件

2. `grep xxx`：从 stdin 中读入若干行数据，如果某行中包含 xxx，则输出该行；否则忽略该行。

3. `wc`：统计行数、单词数、字节数

   - 既可以从 stdin 中直接读入内容；也可以在命令行参数中传入文件名列表

   - `wc -l`：统计行数

   - `wc -w`：统计单词数

   - `wc -c`：统计字节数

4. `tree`：展示当前目录的文件结构
   - `tree /path/to/directory/`：展示某个目录的文件结构

   - `tree -a`：展示隐藏文件

5. `ag xxx`：搜索当前目录下的所有文件，检索 xxx 字符串

6. `cut`：分割一行内容
     - 从 `stdin` 中读入多行数据
     - `echo $PATH | cut -d ':' -f 3,5`：输出 `PATH` 用`:`分割后第 3、5 列数据
     - `echo $PATH | cut -d ':' -f 3-5`：输出 `PATH` 用`:`分割后第 3-5 列数据
     - `echo $PATH | cut -c 3,5`：输出 `PATH` 的第 3、5 个字符
     - `echo $PATH | cut -c 3-5`：输出 `PATH` 的第 3-5 个字符
7. `sort`：将每行内容按字典序排序
     - 可以从 `stdin` 中读取多行数据
     - 可以从命令行参数中读取文件名列表
8. `xargs`：将 `stdin` 中的数据用空格或回车分割成命令行参数
     - `find . -name '*.py' | xargs cat | wc -l`：统计当前目录下所有 python 文件的总行数

#### 查看文件内容

1. `more`：浏览文件内容
   - 回车：下一行
   - 空格：下一页
   - `b`：上一页
   - `q`：退出
2. `less`：与 `more` 类似，功能更全
   - 回车：下一行
   - `y`：上一行
   - `Page Down`：下一页
   - `Page Up`：上一页
   - `q`：退出
3. `head -3 xxx`：展示 xxx 的前3  行内容
   - 同时支持从 `stdin` 读入内容
4. `tail -3 xxx`：展示 xxx 末尾 3 行内容
   - 同时支持从 `stdin` 读入内容

#### 工具

1. `md5sum`：计算 `md5` 哈希值
   - 可以从 `stdin` 读入内容
   - 也可以在命令行参数中传入文件名列表；
2. `time command`：统计 `command` 命令的执行时间
3. `ipython3`：交互式 `python3` 环境。可以当做计算器，或者批量管理文件。
   - `! echo "Hello World"`：`!` 表示执行 `shell` 脚本
4. `watch -n 0.1 command`：每 0.1 秒执行一次 `command` 命令
5. `tar`：压缩文件
   - `tar -zcvf xxx.tar.gz /path/to/file/*`：压缩
   - `tar -zxvf xxx.tar.gz`：解压缩
6. `diff xxx yyy`：查找文件 `xxx` 与 `yyy` 的不同点

#### 安装软件

1. `sudo command`：以 `root` 身份执行 `command` 命令
2. `apt-get install xxx`：安装软件
3. `pip install xxx --user --upgrade`：安装 `python` 包
