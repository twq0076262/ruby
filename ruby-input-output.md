# Ruby 文件的输入与输出

Ruby 提供了一整套 I/O 相关的方法，在内核（Kernel）模块中实现。所有的 I/O 方法派生自 IO 类。

类 _IO_ 提供了所有基础的方法，比如 _read、 write、 gets、 puts、 readline、 getc_ 和 _printf_。

本章节将讲解所有 Ruby 中可用的基础的 I/O 函数。如需了解更多的函数，请查看 Ruby 的 _IO_ 类。

## puts 语句

在前面的章节中，您赋值给变量，然后使用 _puts_ 语句打印输出。

_puts_ 语句指示程序显示存储在变量中的值。这将在每行末尾添加一个新行。

## 实例

```
    #!/usr/bin/ruby

    val1 = "This is variable one"
    val2 = "This is variable two"
    puts val1
    puts val2
```
这将产生以下结果：

```
    This is variable one
    This is variable two
```

## gets 语句
_gets_ 语句可用于获取来自名为 STDIN 的标准屏幕的用户输入。

## 实例

下面的代码演示了如何使用 gets 语句。该代码将提示用户输入一个值，该值将被存储在变量 val 中，最后会被打印在 STDOUT 上。

```
    #!/usr/bin/ruby

    puts "Enter a value :"
    val = gets
    puts val
```

这将产生以下结果：

```
    Enter a value :
    This is entered value
    This is entered value
```

## putc 语句
与 _puts_ 语句不同，_puts_ 语句输出整个字符串到屏幕上，而 _putc_ 语句可用于依次输出一个字符。

## 实例

下面代码的输出只是字符 H：

```
    #!/usr/bin/ruby

    str="Hello Ruby!"
    putc str
```

这将产生以下结果：

```
    H
```

## print 语句
_print_ 语句与 _puts_ 语句类似。唯一的不同在于 _puts_ 语句在输出内容后会跳到下一行，而使用 _print_ 语句时，光标定位在同一行。

## 实例

```
    #!/usr/bin/ruby

    print "Hello World"
    print "Good Morning"
```

这将产生以下结果：

```
    Hello WorldGood Morning
```

## 打开和关闭文件
截至现在，您已经读取并写入标准输入和输出。现在，我们将看看如何操作实际的数据文件。

## _File.new_ 方法

您可以使用 _File.new_ 方法创建一个 _File_ 对象用于读取、写入或者读写，读写权限取决于 mode 字符串。最后，您可以使用 _File.close_ 方法来关闭该文件。

### 语法

```
    aFile = File.new("filename", "mode")
       # ... 处理文件
    aFile.close
```

## _File.open_ 方法

您可以使用 _File.open_ 方法创建一个新的 file 对象，并把该 file 对象赋值给文件。但是，_File.open_ 和 _File.new_ 方法之间有一点不同。不同点是 _File.open_ 方法可与块关联，而 _File.new_ 方法不能。

```
    File.open("filename", "mode") do |aFile|
       # ... process the file
    end
```

下表列出了打开文件的不同模式：


</p> <table > <tr><th>模式</th><th>描述</th></tr> <tr><td>r</td><td>只读模式。文件指针被放置在文件的开头。这是默认模式。</td></tr> <tr><td>r+</td><td>读写模式。文件指针被放置在文件的开头。</td></tr> <tr><td>w</td><td>只写模式。如果文件存在，则重写文件。如果文件不存在，则创建一个新文件用于写入。</td></tr> <tr><td>w+</td><td>读写模式。如果文件存在，则重写已存在的文件。如果文件不存在，则创建一个新文件用于读写。</td></tr> <tr><td>a</td><td>只写模式。如果文件存在，则文件指针被放置在文件的末尾。也就是说，文件是追加模式。如果文件不存在，则创建一个新文件用于写入。</td></tr> <tr><td>a+</td><td>读写模式。如果文件存在，则文件指针被放置在文件的末尾。也就是说，文件是追加模式。如果文件不存在，则创建一个新文件用于读写。</td></tr> </table> <br /> 


## 读取和写入文件

用于简单 I/O 的方法也可用于所有 file 对象。所以，gets 从标准输入读取一行，_aFile.gets_ 从文件对象 aFile 读取一行。

但是，I/O 对象提供了访问方法的附加设置，为我们提供了便利。

## _sysread_ 方法

您可以使用方法 _sysread_ 来读取文件的内容。当使用方法 sysread 时，您可以使用任意一种模式打开文件。例如：

下面是输入文本文件：

```
    This is a simple text file for testing purpose.
```

现在让我们尝试读取这个文件：

```
    #!/usr/bin/ruby
    
    aFile = File.new("input.txt", "r")
    if aFile
       content = aFile.sysread(20)
       puts content
    else
       puts "Unable to open file!"
    end
```

该语句将输入文件的头 20 个字符。文件指针将被放置在文件中第 21 个字符的位置。

## _syswrite_ 方法

您可以使用方法 _syswrite_ 来向文件写入内容。当使用方法 syswrite 时，您需要以写入模式打开文件。例如：

```
    #!/usr/bin/ruby

    aFile = File.new("input.txt", "r+")
    if aFile
       aFile.syswrite("ABCDEF")
    else
       puts "Unable to open file!"
    end
```

该语句将写入 "ABCDEF" 到文件中。

## _each_byte_ 方法

该方法属于类 _File_。方法 _each_byte_ 是个可以迭代字符串中每个字符。请看下面的代码实例：

```
    #!/usr/bin/ruby

    aFile = File.new("input.txt", "r+")
    if aFile
       aFile.syswrite("ABCDEF")
       aFile.rewind
       aFile.each_byte {|ch| putc ch; putc ?. }
    else
       puts "Unable to open file!"
    end
```

字符一个接着一个被传到变量 ch，然后显示在屏幕上，如下所示：


```
A.B.C.D.E.F.s. .a. .s.i.m.p.l.e. .t.e.x.t. .f.i.l.e. .f.o.r. .t.e.s.t.i.n.g. .p.u.r.p.o.s.e...
```

## _IO.readlines_ 方法

类 _File_ 是类 IO 的一个子类。类 IO 也有一些用于操作文件的方法。

_IO.readlines_ 是 IO 类中的一个方法。该方法逐行返回文件的内容。下面的代码显示了方法 _IO.readlines_ 的使用：

```
    #!/usr/bin/ruby

    arr = IO.readlines("input.txt")
    puts arr[0]
    puts arr[1]
```

在这段代码中，变量 arr 是一个数组。文件 _input.txt_ 的每一行将是数组 arr 中的一个元素。因此，arr[0] 将包含第一行，而 arr[1] 将包含文件的第二行。

## _IO.foreach_ 方法

该方法也逐行返回输出。方法 _foreach_ 与方法 _readlines_ 之间不同的是，方法 _foreach_ 与块相关联。但是，不像方法 _readlines_，方法 _foreach_ 不是返回一个数组。例如：

```
    #!/usr/bin/ruby

    IO.foreach("input.txt"){|block| puts block}
```

这段代码将把文件 _test_ 的内容逐行传给变量 block，然后输出将显示在屏幕上。

## 重命名和删除文件

您可以通过 _rename_ 和 _delete_ 方法重命名和删除文件。

下面的实例重命名一个已存在文件 _test1.txt_：

```
    #!/usr/bin/ruby

    # 重命名文件 test1.txt 为 test2.txt
    File.rename( "test1.txt", "test2.txt" )
```

下面的实例删除一个已存在文件 _test2.txt_：

```
    #!/usr/bin/ruby

    # 删除文件 test2.txt
    File.delete("text2.txt")
```

## 文件模式与所有权
使用带有掩码的 _chmod_ 方法来改变文件的模式或权限/访问列表：

下面的实例改变一个已存在文件 _test.txt_ 的模式为一个掩码值：

```
    #!/usr/bin/ruby

    file = File.new( "test.txt", "w" )
    file.chmod( 0755 )
```

下表列出了 _chmod_ 方法中可使用的不同的掩码：

</p> <table > <tr><th style="width:25%">掩码</th><th>描述</th></tr> <tr><td>0700</td><td>rwx 掩码，针对所有者</td></tr> <tr><td>0400</td><td>r ，针对所有者</td></tr> <tr><td>0200</td><td>w ，针对所有者</td></tr> <tr><td>0100</td><td>x ，针对所有者</td></tr> <tr><td>0070</td><td>rwx 掩码，针对所属组</td></tr> <tr><td>0040</td><td>r ，针对所属组</td></tr> <tr><td>0020</td><td>w ，针对所属组</td></tr> <tr><td>0010</td><td>x ，针对所属组</td></tr> <tr><td>0007</td><td>rwx 掩码，针对其他人</td></tr> <tr><td>0004</td><td>r ，针对其他人</td></tr> <tr><td>0002</td><td>w ，针对其他人</td></tr> <tr><td>0001</td><td>x ，针对其他人</td></tr> <tr><td>4000</td><td>执行时设置用户 ID</td></tr> <tr><td>2000</td><td>执行时设置所属组 ID</td></tr> <tr><td>1000</td><td>保存交换文本，甚至在使用后也会保存</td></tr> </table> <br /> 


## 文件查询

下面的命令在打开文件前检查文件是否已存在：

```
    #!/usr/bin/ruby

    File.open("file.rb") if File::exists?( "file.rb" )
```

下面的命令查询文件是否确实是一个文件：

```
    #!/usr/bin/ruby

    # 返回 true 或false
    File.file?( "text.txt" )
```

下面的命令检查给定的文件名是否是一个目录：

```
    #!/usr/bin/ruby

    # 一个目录
    File::directory?( "/usr/local/bin" ) # => true

    # 一个文件
    File::directory?( "file.rb" ) # => false
```

下面的命令检查文件是否可读、可写、可执行：

```
    #!/usr/bin/ruby

    File.readable?( "test.txt" )   # => true
    File.writable?( "test.txt" )   # => true
    File.executable?( "test.txt" ) # => false
```

下面的命令检查文件是否大小为零：

```
    #!/usr/bin/ruby

    File.zero?( "test.txt" )      # => true
```

下面的命令返回文件的大小：

```
    #!/usr/bin/ruby

    File.size?( "text.txt" )     # => 1002
```

下面的命令用于检查文件的类型：

```
    #!/usr/bin/ruby

    File::ftype( "test.txt" )     # => file
```

ftype 方法通过返回下列中的某个值来标识了文件的类型：_file、 directory、 characterSpecial、 blockSpecial、 fifo、 link、 socket 或 unknown_。

下面的命令用于检查文件被创建、修改或最后访问的时间：

```
    #!/usr/bin/ruby

    File::ctime( "test.txt" ) # => Fri May 09 10:06:37 -0700 2008
    File::mtime( "text.txt" ) # => Fri May 09 10:44:44 -0700 2008
    File::atime( "text.txt" ) # => Fri May 09 10:45:01 -0700 2008
```

## Ruby 中的目录

所有的文件都是包含在目录中，Ruby 提供了处理文件和目录的方式。_File_ 类用于处理文件，_Dir_ 类用于处理目录。

## 浏览目录

为了在 Ruby 程序中改变目录，请使用 _Dir.chdir_。下面的实例改变当前目录为 _/usr/bin_。

```
    Dir.chdir("/usr/bin")
```

您可以通过_ Dir.pwd_ 查看当前目录：

```
    puts Dir.pwd # 返回当前目录，类似 /usr/bin
```

您可以使用 _Dir.entries_ 获取指定目录内的文件和目录列表：

```
    puts Dir.entries("/usr/bin").join(' ')
```

_Dir.entries_ 返回一个数组，包含指定目录内的所有项。_Dir.foreach_ 提供了相同的功能：

```
    Dir.foreach("/usr/bin") do |entry|
       puts entry
    end
```

获取目录列表的一个更简洁的方式是通过使用 Dir 的类数组的方法：

```
    Dir["/usr/bin/*"]
```

## 创建目录

_Dir.mkdir_ 可用于创建目录：

```
    Dir.mkdir("mynewdir")
```

您也可以通过 mkdir 在新目录（不是已存在的目录）上设置权限：

**注意：**掩码 755 设置所有者（owner）、所属组（group）、每个人（world [anyone]）的权限为 rwxr-xr-x，其中 r = read 读取，w = write 写入，x = execute 执行。

```
    Dir.mkdir( "mynewdir", 755 )
```

## 删除目录

_Dir.delete_ 可用于删除目录。_Dir.unlink_ 和 _Dir.rmdir_ 执行同样的功能，为我们提供了便利。

```
    Dir.delete("testdir")
```

## 创建文件 & 临时目录

临时文件是那些在程序执行过程中被简单地创建，但不会永久性存储的信息。

_Dir.tmpdir_ 提供了当前系统上临时目录的路径，但是该方法默认情况下是不可用的。为了让 _Dir.tmpdir_ 可用，使用必需的 'tmpdir' 是必要的。

您可以把 _Dir.tmpdir_ 和 _File.join_ 一起使用，来创建一个独立于平台的临时文件：

```
    require 'tmpdir'
       tempfilename = File.join(Dir.tmpdir, "tingtong")
       tempfile = File.new(tempfilename, "w")
       tempfile.puts "This is a temporary file"
       tempfile.close
       File.delete(tempfilename)
```

这段代码创建了一个临时文件，并向其中写入数据，然后删除文件。Ruby 的标准库也包含了一个名为 _Tempfile_ 的库，该库可用于创建临时文件：

```
    require 'tempfile'
       f = Tempfile.new('tingtong')
       f.puts "Hello"
       puts f.path
       f.close
```

## 内建函数
下面提供了 Ruby 中处理文件和目录的内建函数的完整列表：

[File 类和方法](ruby-file-methods.md)

[Dir 类和方法](ruby-dir-methods.md)
