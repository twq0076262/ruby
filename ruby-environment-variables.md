# Ruby 环境变量

Ruby 解释器使用下列环境变量来控制它的行为。ENV 对象包含了所有当前设置的环境变量列表。

</p> <table > <tr><th>变量</th><th>描述</th></tr> <tr><td><b>DLN_LIBRARY_PATH</b></td><td> 动态加载模块搜索的路径。</td></tr> <tr><td><b>HOME</b></td><td> 当没有参数传递给 Dir::chdir 时，要移动到的目录。也用于 File::expand_path 来扩展 "~"。</td></tr> <tr><td><b>LOGDIR</b></td><td> 当没有参数传递给 Dir::chdir 且未设置环境变量 HOME 时，要移动到的目录。</td></tr> <tr><td><b>PATH</b></td><td> 执行子进程的搜索路径，以及在指定 -S 选项后，Ruby 程序的搜索路径。每个路径用冒号分隔（在 DOS 和 Windows 中用分号分隔）。</td></tr> <tr><td><b>RUBYLIB</b></td><td> 库的搜索路径。每个路径用冒号分隔（在 DOS 和 Windows 中用分号分隔）。</td></tr> <tr><td><b>RUBYLIB_PREFIX</b></td><td> 用于修改 RUBYLIB 搜索路径，通过使用格式 path1;path2 或 path1path2，把库的前缀 path1 替换为 path2。</td></tr> <tr><td><b>RUBYOPT</b></td><td> 传给 Ruby 解释器的命令行选项。在 taint 模式时被忽略（其中，$SAFE 大于 0）。</td></tr> <tr><td><b>RUBYPATH</b></td><td> 指定 -S 选项后，Ruby 程序的搜索路径。优先级高于 PATH。在 taint 模式时被忽略（其中，$SAFE 大于 0）。</td></tr> <tr><td><b>RUBYSHELL</b></td><td> 指定执行命令时所使用的 shell。如果未设置该环境变量，则使用 SHELL 或 COMSPEC。</td></tr> </table> <p>

对于 Unix，使用 env 命令来查看所有环境变量的列表。

```
HOSTNAME=ip-72-167-112-17.ip.secureserver.net
RUBYPATH=/usr/bin
SHELL=/bin/bash
TERM=xterm
HISTSIZE=1000
SSH_CLIENT=122.169.131.179 1742 22
SSH_TTY=/dev/pts/1
USER=amrood
JRE_HOME=/usr/java/jdk/jre
J2RE_HOME=/usr/java/jdk/jre
PATH=/usr/local/bin:/bin:/usr/bin:/home/guest/bin
MAIL=/var/spool/mail/guest
PWD=/home/amrood
INPUTRC=/etc/inputrc
JAVA_HOME=/usr/java/jdk
LANG=C
HOME=/root
SHLVL=2
JDK_HOME=/usr/java/jdk
LOGDIR=/usr/log/ruby
LOGNAME=amrood
SSH_CONNECTION=122.169.131.179 1742 72.167.112.17 22
LESSOPEN=|/usr/bin/lesspipe.sh %s
RUBYLIB=/usr/lib/ruby
G_BROKEN_FILENAMES=1
_=/bin/env
```