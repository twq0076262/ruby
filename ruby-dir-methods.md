# Ruby Dir 类和方法


**Dir** 是一个表示用于给出操作系统中目录中的文件名的目录流。Dir 类也拥有与目录相关的操作，比如通配符文件名匹配、改变工作目录等。


## 类方法


<table > <tr><th style="width:5%">序号</th><th>方法 & 描述</th></tr> <tr><td>1</td><td><b>Dir[pat]<br /> Dir::glob( pat)</b><br />返回一个数组，包含与指定的通配符模式 pat 匹配的文件名： <ul > <li><b>*</b> - 匹配包含 null 字符串的任意字符串</li> <li><b>**</b> - 递归地匹配任意字符串</li> <li><b>?</b> - 匹配任意单个字符</li> <li><b>[...]</b> - 匹配封闭字符中的任意一个</li> <li><b></b> - 匹配字符串中的任意一个</li> </ul> Dir["foo.*"] # 匹配 "foo.c"、 "foo.rb" 等等<br /> Dir["foo.?"] # 匹配 "foo.c"、 "foo.h" 等等 </td></tr> <tr><td>2</td><td><b>Dir::chdir( path)</b><br />改变当前目录。</td></tr> <tr><td>3</td><td><b>Dir::chroot( path)</b><br />改变根目录（只允许超级用户）。并不是在所有的平台上都可用。</td></tr> <tr><td>4</td><td><b>Dir::delete( path)</b><br />删除 path 指定的目录。目录必须是空的。</td></tr> <tr><td>5</td><td><b>Dir::entries( path)</b><br />返回一个数组，包含目录 path 中的文件名。</td></tr> <tr><td>6</td><td><b>Dir::foreach( path) {| f| ...}</b><br />为 path 指定的目录中的每个文件执行一次块。</td></tr> <tr><td>7</td><td><b>Dir::getwd<br /> Dir::pwd</b><br />返回当前目录。</td></tr> <tr><td>8</td><td><b>Dir::mkdir( path[, mode=0777])</b><br />创建 path 指定的目录。权限模式可被 File::umask 的值修改，在 Win32 的平台上会被忽略。</td></tr> <tr><td>9</td><td><b>Dir::new( path)<br /> Dir::open( path)<br /> Dir::open( path) {| dir| ...}</b><br />返回 path 的新目录对象。如果 open 给出一个块，则新目录对象会传到该块，块会在终止前关闭目录对象。</td></tr> <tr><td>10</td><td><b>Dir::pwd</b><br />参见 Dir::getwd。</td></tr> <tr><td>11</td><td><b>Dir::rmdir( path)<br /> Dir::unlink( path)<br /> Dir::delete( path)</b><br />删除 path 指定的目录。目录必须是空的。</td></tr> </table> 

## 实例方法

假设 **d** 是 **Dir** 类的一个实例：

</p> <table > <tr><th style="width:5%">序号</th><th>方法 & 描述</th></tr> <tr><td>1</td><td><b>d.close</b><br />关闭目录流。</td></tr> <tr><td>2</td><td><b>d.each {| f| ...}</b><br />为 d 中的每一个条目执行一次块。</td></tr> <tr><td>3</td><td><b>d.pos</b><br /> d.tell<br />返回 d 中的当前位置。</td></tr> <tr><td>4</td><td><b>d.pos= offset</b><br />设置目录流中的位置。</td></tr> <tr><td>5</td><td><b>d.pos= pos<br /> d.seek(pos)</b><br />移动到 d 中的某个位置。pos 必须是一个由 d.pos 返回的值或 0。</td></tr> <tr><td>6</td><td><b>d.read</b><br />返回 d 的下一个条目。</td></tr> <tr><td>7</td><td><b>d.rewind</b><br />移动 d 中的位置到第一个条目。</td></tr> <tr><td>8</td><td><b>d.seek(po s)</b><br />参见 d.pos=pos。</td></tr> <tr><td>9</td><td><b>d.tell</b><br />参见 d.pos。</td></tr> </table> 