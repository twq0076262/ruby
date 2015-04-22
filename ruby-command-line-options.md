# Ruby 命令行选项

Ruby 一般是从命令行运行，方式如下：

```
$ ruby [ options ] [.] [ programfile ] [ arguments ... ]
```

解释器可以通过下列选项被调用，来控制解释器的环境和行为。

</p> <table > <tr><th width="15%">选项</th><th>描述</th></tr> <tr><td><b>-a</b></td><td> 与 -n 或 -p 一起使用时，可以打开自动拆分模式(auto split mode)。请查看 -n 和 -p 选项。</td></tr> <tr><td><b>-c</b></td><td> 只检查语法，不执行程序。</td></tr> <tr><td><b>-C dir</b></td><td> 在执行前改变目录（等价于 -X）。</td></tr> <tr><td><b>-d</b></td><td> 启用调试模式（等价于 -debug）。</td></tr> <tr><td><b>-F pat</b></td><td> 指定 pat 作为默认的分离模式（$;）。</td></tr> <tr><td><b>-e prog</b></td><td> 指定 prog 作为程序在命令行中执行。可以指定多个 -e 选项，用来执行多个程序。</td></tr> <tr><td><b>-h</b></td><td> 显示命令行选项的一个概览。</td></tr> <tr><td><b>-i [ ext]</b></td><td> 把文件内容重写为程序输出。原始文件会被加上扩展名 ext 保存下来。如果未指定 ext，原始文件会被删除。</td></tr> <tr><td><b>-I dir</b></td><td> 添加 dir 作为加载库的目录。</td></tr> <tr><td><b>-K [ kcode]</b></td><td> 指定多字节字符集编码。e 或 E 对应 EUC（extended Unix code），s 或 S 对应 SJIS（Shift-JIS），u 或 U 对应 UTF-8，a、A、n 或 N 对应 ASCII。</td></tr> <tr><td><b>-l</b></td><td> 启用自动行尾处理。从输入行取消一个换行符，并向输出行追加一个换行符。</td></tr> <tr><td><b>-n</b></td><td> 把代码放置在一个输入循环中（就像在 while gets; ... end 中一样）。</td></tr> <tr><td><b>-0[ octal]</b></td><td> 设置默认的记录分隔符（$/）为八进制。如果未指定 octal 则默认为 \0。</td></tr> <tr><td><b>-p</b></td><td> 把代码放置在一个输入循环中。在每次迭代后输出变量 $_ 的值。</td></tr> <tr><td><b>-r lib</b></td><td> 使用 <i>require</i> 来加载 <i>lib</i> 作为执行前的库。</td></tr> <tr><td><b>-s</b></td><td> 解读程序名称和文件名参数之间的匹配模式 -xxx 的任何参数作为开关，并定义相应的变量。</td></tr> <tr><td><b>-T [level]</b></td><td> 设置安全级别，执行不纯度测试（如果未指定 level，则默认值为 1）。</td></tr> <tr><td><b>-v</b></td><td> 显示版本，并启用冗余模式。</td></tr> <tr><td><b>-w</b></td><td> 启用冗余模式。如果未指定程序文件，则从 STDIN 读取。</td></tr> <tr><td><b>-x [dir]</b></td><td> 删除 #!ruby 行之前的文本。如果指定了 <i>dir</i>，则把目录改变为 <i>dir</i>。</td></tr> <tr><td><b>-X dir</b></td><td> 在执行前改变目录（等价于 -C）。</td></tr> <tr><td><b>-y</b></td><td> 启用解析器调试模式。</td></tr> <tr><td><b>--copyright</b></td><td> 显示版权声明。</td></tr> <tr><td><b>--debug</b></td><td> 启用调试模式（等价于 -d）。</td></tr> <tr><td><b>--help</b></td><td> 显示命令行选项的一个概览（等价于 -h）。</td></tr> <tr><td><b>--version</b></td><td> 显示版本。</td></tr> <tr><td><b>--verbose</b></td><td> 启用冗余模式（等价于 -v）。设置 $VERBOSE 为 true。</td></tr> <tr><td><b>--yydebug</b></td><td> 启用解析器调试模式（等价于 -y）。</td></tr> </table> <p>

单字符的命令行选项可以组合使用。下面两行表达了同样的意思：

```
$ruby -ne 'print if /Ruby/' /usr/share/bin


$ruby -n -e 'print if /Ruby/' /usr/share/bin
```