# linux_study
## 1.常用文件管理命令
```
(1) ctrl c: 取消命令，并且换行
(2) ctrl u: 清空本行命令
(3) tab键：可以补全命令和文件名，如果补全不了快速按两下tab键，可以显示备选选项
(4) ls: 列出当前目录下所有文件，蓝色的是文件夹，白色的是普通文件，绿色的是可执行文件
(5) pwd: 显示当前路径
(6) cd XXX: 进入XXX目录下, cd .. 返回上层目录
(7) cp XXX YYY: 将XXX文件复制成YYY，XXX和YYY可以是一个路径，比如../dir_c/a.txt，表示上层目录下的dir_c文件夹下的文件a.txt
(8) mkdir XXX: 创建目录XXX
(9) rm XXX: 删除普通文件;  rm XXX -r: 删除文件夹
(10) mv XXX YYY: 将XXX文件移动到YYY，和cp命令一样，XXX和YYY可以是一个路径；重命名也是用这个命令
(11) touch XXX: 创建一个文件
(12) cat XXX: 展示文件XXX中的内容
(13) 复制文本
    windows/Linux下：Ctrl + insert，Mac下：command + c
(14) 粘贴文本
    windows/Linux下：Shift + insert，Mac下：command + v
```
环境变量概念

Linux系统中会用很多环境变量来记录配置信息。
环境变量类似于全局变量，可以被各个进程访问到。我们可以通过修改环境变量来方便地修改系统配置。

查看

列出当前环境下的所有环境变量：

env  # 显示当前用户的变量
set  # 显示当前shell的变量，包括当前用户的变量;
export  # 显示当前导出成用户变量的shell变量
输出某个环境变量的值：

echo $PATH
修改

环境变量的定义、修改、删除操作可以参考3. shell语法——变量这一节的内容。

为了将对环境变量的修改应用到未来所有环境下，可以将修改命令放到~/.bashrc文件中。
修改完~/.bashrc文件后，记得执行source ~/.bashrc，来将修改应用到当前的bash环境下。

为何将修改命令放到~/.bashrc，就可以确保修改会影响未来所有的环境呢？

每次启动bash，都会先执行~/.bashrc。
每次ssh登陆远程服务器，都会启动一个bash命令行给我们。
每次tmux新开一个pane，都会启动一个bash命令行给我们。
所以未来所有新开的环境都会加载我们修改的内容。
常见环境变量

HOME：用户的家目录。
PATH：可执行文件（命令）的存储路径。路径与路径之间用:分隔。当某个可执行文件同时出现在多个路径中时，会选择从左到右数第一个路径中的执行。下列所有存储路径的环境变量，均采用从左到右的优先顺序。
LD_LIBRARY_PATH：用于指定动态链接库(.so文件)的路径，其内容是以冒号分隔的路径列表。
C_INCLUDE_PATH：C语言的头文件路径，内容是以冒号分隔的路径列表。
CPLUS_INCLUDE_PATH：CPP的头文件路径，内容是以冒号分隔的路径列表。
PYTHONPATH：Python导入包的路径，内容是以冒号分隔的路径列表。
JAVA_HOME：jdk的安装目录。
CLASSPATH：存放Java导入类的路径，内容是以冒号分隔的路径列表。

系统状况

top：查看所有进程的信息（Linux的任务管理器）
打开后，输入M：按使用内存排序
打开后，输入P：按使用CPU排序
打开后，输入q：退出
df -h：查看硬盘使用情况
free -h：查看内存使用情况
du -sh：查看当前目录占用的硬盘空间
ps aux：查看所有进程
kill -9 pid：杀死编号为pid的进程
传递某个具体的信号：kill -s SIGTERM pid
netstat -nt：查看所有网络连接
w：列出当前登陆的用户
ping www.baidu.com：检查是否连网
文件权限

chmod：修改文件权限
chmod +x xxx：给xxx添加可执行权限
chmod -x xxx：去掉xxx的可执行权限
chmod 777 xxx：将xxx的权限改成777
chmod 777 xxx -R：递归修改整个文件夹的权限
文件检索

find /path/to/directory/ -name '*.py'：搜索某个文件路径下的所有*.py文件
grep xxx：从stdin中读入若干行数据，如果某行中包含xxx，则输出该行；否则忽略该行。
wc：统计行数、单词数、字节数
既可以从stdin中直接读入内容；也可以在命令行参数中传入文件名列表；
wc -l：统计行数
wc -w：统计单词数
wc -c：统计字节数
tree：展示当前目录的文件结构
tree /path/to/directory/：展示某个目录的文件结构
tree -a：展示隐藏文件
ag xxx：搜索当前目录下的所有文件，检索xxx字符串
cut：分割一行内容
从stdin中读入多行数据
echo $PATH | cut -d ':' -f 3,5：输出PATH用:分割后第3、5列数据
echo $PATH | cut -d ':' -f 3-5：输出PATH用:分割后第3-5列数据
echo $PATH | cut -c 3,5：输出PATH的第3、5个字符
echo $PATH | cut -c 3-5：输出PATH的第3-5个字符
sort：将每行内容按字典序排序
可以从stdin中读取多行数据
可以从命令行参数中读取文件名列表
xargs：将stdin中的数据用空格或回车分割成命令行参数
find . -name '*.py' | xargs cat | wc -l：统计当前目录下所有python文件的总行数
查看文件内容

more：浏览文件内容
回车：下一行
空格：下一页
b：上一页
q：退出
less：与more类似，功能更全
回车：下一行
y：上一行
Page Down：下一页
Page Up：上一页
q：退出
head -3 xxx：展示xxx的前3行内容
同时支持从stdin读入内容
tail -3 xxx：展示xxx末尾3行内容
同时支持从stdin读入内容
用户相关

history：展示当前用户的历史操作。内容存放在~/.bash_history中
工具

md5sum：计算md5哈希值
可以从stdin读入内容
也可以在命令行参数中传入文件名列表；
time command：统计command命令的执行时间
ipython3：交互式python3环境。可以当做计算器，或者批量管理文件。
! echo "Hello World"：!表示执行shell脚本
watch -n 0.1 command：每0.1秒执行一次command命令
tar：压缩文件
tar -zcvf xxx.tar.gz /path/to/file/*：压缩
tar -zxvf xxx.tar.gz：解压缩
diff xxx yyy：查找文件xxx与yyy的不同点
安装软件

sudo command：以root身份执行command命令
apt-get install xxx：安装软件
pip install xxx --user --upgrade：安装python包

管道概念

管道类似于文件重定向，可以将前一个命令的stdout重定向到下一个命令的stdin。

要点

管道命令仅处理stdout，会忽略stderr。
管道右边的命令必须能接受stdin。
多个管道命令可以串联。
与文件重定向的区别

文件重定向左边为命令，右边为文件。
管道左右两边均为命令，左边有stdout，右边有stdin。
举例

统计当前目录下所有python文件的总行数，其中find、xargs、wc等命令可以参考常用命令这一节内容。

find . -name '*.py' | xargs cat | wc -l

## 2.tmux和vim
### 1. tmux教程
```
功能：
    (1) 分屏。
    (2) 允许断开Terminal连接后，继续运行进程。
结构：
    一个tmux可以包含多个session，一个session可以包含多个window，一个window可以包含多个pane。
    实例：
        tmux:
            session 0:
                window 0:
                    pane 0
                    pane 1
                    pane 2
                    ...
                window 1
                window 2
                ...
            session 1
            session 2
            ...
操作：
    (1) tmux：新建一个session，其中包含一个window，window中包含一个pane，pane里打开了一个shell对话框。
    (2) 按下Ctrl + a后手指松开，然后按%：将当前pane左右平分成两个pane。
    (3) 按下Ctrl + a后手指松开，然后按"（注意是双引号"）：将当前pane上下平分成两个pane。
    (4) Ctrl + d：关闭当前pane；如果当前window的所有pane均已关闭，则自动关闭window；如果当前session的所有window均已关闭，则自动关闭session。
    (5) 鼠标点击可以选pane。
    (6) 按下ctrl + a后手指松开，然后按方向键：选择相邻的pane。
    (7) 鼠标拖动pane之间的分割线，可以调整分割线的位置。
    (8) 按住ctrl + a的同时按方向键，可以调整pane之间分割线的位置。
    (9) 按下ctrl + a后手指松开，然后按z：将当前pane全屏/取消全屏。
    (10) 按下ctrl + a后手指松开，然后按d：挂起当前session。
    (11) tmux a：打开之前挂起的session。
    (12) 按下ctrl + a后手指松开，然后按s：选择其它session。
        方向键 —— 上：选择上一项 session/window/pane
        方向键 —— 下：选择下一项 session/window/pane
        方向键 —— 右：展开当前项 session/window
        方向键 —— 左：闭合当前项 session/window
    (13) 按下Ctrl + a后手指松开，然后按c：在当前session中创建一个新的window。
    (14) 按下Ctrl + a后手指松开，然后按w：选择其他window，操作方法与(12)完全相同。
    (15) 按下Ctrl + a后手指松开，然后按PageUp：翻阅当前pane内的内容。
    (16) 鼠标滚轮：翻阅当前pane内的内容。
    (17) 在tmux中选中文本时，需要按住shift键。（仅支持Windows和Linux，不支持Mac，不过该操作并不是必须的，因此影响不大）
    (18) tmux中复制/粘贴文本的通用方式：
        (1) 按下Ctrl + a后松开手指，然后按[
        (2) 用鼠标选中文本，被选中的文本会被自动复制到tmux的剪贴板
        (3) 按下Ctrl + a后松开手指，然后按]，会将剪贴板中的内容粘贴到光标处
```
### 2. vim教程
```
功能：
    (1) 命令行模式下的文本编辑器。
    (2) 根据文件扩展名自动判别编程语言。支持代码缩进、代码高亮等功能。
    (3) 使用方式：vim filename
        如果已有该文件，则打开它。
        如果没有该文件，则打开个一个新的文件，并命名为filename
模式：
    (1) 一般命令模式
        默认模式。命令输入方式：类似于打游戏放技能，按不同字符，即可进行不同操作。可以复制、粘贴、删除文本等。
    (2) 编辑模式
        在一般命令模式里按下i，会进入编辑模式。
        按下ESC会退出编辑模式，返回到一般命令模式。
    (3) 命令行模式
        在一般命令模式里按下:/?三个字母中的任意一个，会进入命令行模式。命令行在最下面。
        可以查找、替换、保存、退出、配置编辑器等。
操作：
    (1) i：进入编辑模式
    (2) ESC：进入一般命令模式
    (3) h 或 左箭头键：光标向左移动一个字符
    (4) j 或 向下箭头：光标向下移动一个字符
    (5) k 或 向上箭头：光标向上移动一个字符
    (6) l 或 向右箭头：光标向右移动一个字符
    (7) n<Space>：n表示数字，按下数字后再按空格，光标会向右移动这一行的n个字符
    (8) 0 或 功能键[Home]：光标移动到本行开头
    (9) $ 或 功能键[End]：光标移动到本行末尾
    (10) G：光标移动到最后一行
    (11) :n 或 nG：n为数字，光标移动到第n行
    (12) gg：光标移动到第一行，相当于1G
    (13) n<Enter>：n为数字，光标向下移动n行
    (14) /word：向光标之下寻找第一个值为word的字符串。
    (15) ?word：向光标之上寻找第一个值为word的字符串。
    (16) n：重复前一个查找操作
    (17) N：反向重复前一个查找操作
    (18) :n1,n2s/word1/word2/g：n1与n2为数字，在第n1行与n2行之间寻找word1这个字符串，并将该字符串替换为word2
    (19) :1,$s/word1/word2/g：将全文的word1替换为word2
    (20) :1,$s/word1/word2/gc：将全文的word1替换为word2，且在替换前要求用户确认。
    (21) v：选中文本
    (22) d：删除选中的文本
    (23) dd: 删除当前行
    (24) y：复制选中的文本
    (25) yy: 复制当前行
    (26) p: 将复制的数据在光标的下一行/下一个位置粘贴
    (27) u：撤销
    (28) Ctrl + r：取消撤销
    (29) 大于号 >：将选中的文本整体向右缩进一次
    (30) 小于号 <：将选中的文本整体向左缩进一次
    (31) :w 保存
    (32) :w! 强制保存
    (33) :q 退出
    (34) :q! 强制退出
    (35) :wq 保存并退出
    (36) :set paste 设置成粘贴模式，取消代码自动缩进
    (37) :set nopaste 取消粘贴模式，开启代码自动缩进
    (38) :set nu 显示行号
    (39) :set nonu 隐藏行号
    (40) gg=G：将全文代码格式化
    (41) :noh 关闭查找关键词高亮
    (42) Ctrl + q：当vim卡死时，可以取消当前正在执行的命令
异常处理：
    每次用vim编辑文件时，会自动创建一个.filename.swp的临时文件。
    如果打开某个文件时，该文件的swp文件已存在，则会报错。此时解决办法有两种：
        (1) 找到正在打开该文件的程序，并退出
        (2) 直接删掉该swp文件即可
```
## 3.ssh
### ssh登录
基本用法
远程登录服务器：
```
ssh user@hostname
```
user: 用户名
hostname: IP地址或域名
第一次登录时会提示：
```
The authenticity of host '123.57.47.211 (123.57.47.211)' can't be established.
ECDSA key fingerprint is SHA256:iy237yysfCe013/l+kpDGfEG9xxHxm0dnxnAbJTPpG8.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
输入yes，然后回车即可。
这样会将该服务器的信息记录在~/.ssh/known_hosts文件中。

然后输入密码即可登录到远程服务器中。

默认登录端口号为22。如果想登录某一特定端口：
```
ssh user@hostname -p 22
```
配置文件
```
创建文件 ~/.ssh/config
```

然后在文件中输入：
```
Host myserver1
    HostName IP地址或域名
    User 用户名

Host myserver2
    HostName IP地址或域名
    User 用户名
```
之后再使用服务器时，可以直接使用别名myserver1、myserver2。

密钥登录
创建密钥：
```
ssh-keygen
```
然后一直回车即可。

执行结束后，~/.ssh/目录下会多两个文件：
```
id_rsa：私钥
id_rsa.pub：公钥
```
之后想免密码登录哪个服务器，就将公钥传给哪个服务器即可。

例如，想免密登录myserver服务器。则将公钥中的内容，复制到myserver中的~/.ssh/authorized_keys文件里即可。

也可以使用如下命令一键添加公钥：
```
ssh-copy-id myserver
```
执行命令
命令格式：
```
ssh user@hostname command
```
例如：
```
ssh user@hostname ls -a
```
或者

单引号中的$i可以求值
```
ssh myserver 'for ((i = 0; i < 10; i ++ )) do echo $i; done'
```
或者

双引号中的$i不可以求值
```
ssh myserver "for ((i = 0; i < 10; i ++ )) do echo $i; done"
```
### scp传文件
命令格式：
```
scp source destination
```
将source路径下的文件复制到destination中

一次复制多个文件：
```
scp source1 source2 destination
```
复制文件夹：
```
scp -r ~/tmp myserver:/home/acs/
```
将本地家目录中的tmp文件夹复制到myserver服务器中的/home/acs/目录下。
```
scp -r ~/tmp myserver:homework/
```
将本地家目录中的tmp文件夹复制到myserver服务器中的~/homework/目录下。
```
scp -r myserver:homework
````
将myserver服务器中的~/homework/文件夹复制到本地的当前路径下。

指定服务器的端口号：
```
scp -P 22 source1 source2 destination
```
注意： scp的-r -P等参数尽量加在source和destination之前。

使用scp配置其他服务器的vim和tmux
```
scp ~/.vimrc ~/.tmux.conf myserver:
```
## 4.shell
<https://github.com/jona54/linux_study/blob/main/shell_study.md>
## 5.git
<https://github.com/jona54/linux_study/blob/main/git_study.md>
