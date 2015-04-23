# Ruby 正则表达式


**正则表达式**是一种特殊序列的字符，它通过使用有专门语法的模式来匹配或查找其他字符串或字符串集合。


## 语法

**正则表达式**从字面上看是一种介于斜杠之间或介于跟在 %r 后的任意分隔符之间的模式，如下所示：

```
/pattern/
/pattern/im    # 可以指定选项
%r!/usr/local! # 一般的分隔的正则表达式
```

## 实例

```
#!/usr/bin/ruby

line1 = "Cats are smarter than dogs";
line2 = "Dogs also like meat";

if ( line1 =~ /Cats(.*)/ )
  puts "Line1 contains Cats"
end
if ( line2 =~ /Cats(.*)/ )
  puts "Line2 contains  Dogs"
end
```

这将产生以下结果：

```
Line1 contains Cats
```

## 正则表达式修饰符

正则表达式从字面上看可能包含一个可选的修饰符，用于控制各方面的匹配。修饰符在第二个斜杠字符后指定，如上面实例所示。下标列出了 可能的修饰符：

</p> <table > <tr><th style="width:25%">修饰符</th><th>描述</th></tr> <tr><td>i</td><td>当匹配文本时忽略大小写。</td></tr> <tr><td>o</td><td>只执行一次 #{} 插值，正则表达式在第一次时就进行判断。</td></tr> <tr><td>x</td><td>忽略空格，允许在正则表达式中进行注释。</td></tr> <tr><td>m</td><td>匹配多行，把换行字符识别为正常字符。</td></tr> <tr><td>u,e,s,n</td><td>把正则表达式解释为 Unicode（UTF-8）、EUC、SJIS 或 ASCII。如果没有指定修饰符，则认为正则表达式使用的是源编码。</td></tr> </table> <p>

就像字符串通过 %Q 进行分隔一样，Ruby 允许您以 %r 作为正则表达式的开头，后面跟着任意分隔符。这在描述包含大量您不想转义的斜杠字符时非常有用。

```
# 下面匹配单个斜杠字符，不转义
%r|/|               

# Flag 字符可通过下面的语法进行匹配
%r[</(.*)>]i  
```

## 正则表达式模式

除了控制字符，**(+ ? . * ^ $ ( ) [ ] { } | \)**，其他所有字符都匹配本身。您可以通过在控制字符前放置一个反斜杠来对控制字符进行转义。

下表列出了 Ruby 中可用的正则表达式语法。

</p> <table > <tr><th style="width:25%">模式</th><th>描述</th></tr> <tr><td>^</td><td>匹配行的开头。</td></tr> <tr><td>$</td><td>匹配行的结尾。</td></tr> <tr><td>.</td><td>匹配除了换行符以外的任意单字符。使用 m 选项时，它也可以匹配换行符。</td></tr> <tr><td>[...]</td><td>匹配在方括号中的任意单字符。</td></tr> <tr><td>[^...]</td><td>匹配不在方括号中的任意单字符。</td></tr> <tr><td>re*</td><td>匹配前面的子表达式零次或多次。</td></tr> <tr><td>re+</td><td>匹配前面的子表达式一次或多次。</td></tr> <tr><td>re?</td><td>匹配前面的子表达式零次或一次。</td></tr> <tr><td>re{ n}</td><td>匹配前面的子表达式 n 次。</td></tr> <tr><td>re{ n,}</td><td>匹配前面的子表达式 n 次或 n 次以上。</td></tr> <tr><td>re{ n, m}</td><td>匹配前面的子表达式至少 n 次至多 m 次。</td></tr> <tr><td>a| b</td><td>匹配 a 或 b。</td></tr> <tr><td>(re)</td><td>对正则表达式进行分组，并记住匹配文本。</td></tr> <tr><td>(?imx)</td><td>暂时打开正则表达式内的 i、 m 或 x 选项。如果在圆括号中，则只影响圆括号内的部分。</td></tr> <tr><td>(?-imx)</td><td>暂时关闭正则表达式内的 i、 m 或 x 选项。如果在圆括号中，则只影响圆括号内的部分。</td></tr> <tr><td>(?: re)</td><td>对正则表达式进行分组，但不记住匹配文本。</td></tr> <tr><td>(?imx: re)</td><td>暂时打开圆括号内的 i、 m 或 x 选项。</td></tr> <tr><td>(?-imx: re)</td><td>暂时关闭圆括号内的 i、 m 或 x 选项。</td></tr> <tr><td>(?#...)</td><td>注释。</td></tr> <tr><td>(?= re)</td><td>使用模式指定位置。没有范围。</td></tr> <tr><td>(?! re)</td><td>使用模式的否定指定位置。没有范围。</td></tr> <tr><td>(?&gt; re)</td><td>匹配无回溯的独立模式。</td></tr> <tr><td>\w</td><td>匹配单词字符。</td></tr> <tr><td>\W</td><td>匹配非单词字符。</td></tr> <tr><td>\s</td><td>匹配空白字符。等价于 [\t\n\r\f]。</td></tr> <tr><td>\S</td><td>匹配非空白字符。</td></tr> <tr><td>\d</td><td>匹配数字。等价于 [0-9]。</td></tr> <tr><td>\D</td><td>匹配非数字。</td></tr> <tr><td>\A</td><td>匹配字符串的开头。</td></tr> <tr><td>\Z</td><td>匹配字符串的结尾。如果存在换行符，则只匹配到换行符之前。</td></tr> <tr><td>\z</td><td>匹配字符串的结尾。</td></tr> <tr><td>\G</td><td>匹配最后一个匹配完成的点。</td></tr> <tr><td>\b</td><td>当在括号外时匹配单词边界，当在括号内时匹配退格键（0x08）。</td></tr> <tr><td>\B</td><td>匹配非单词边界。</td></tr> <tr><td>\n, \t, etc.</td><td>匹配换行符、回车符、制表符，等等。</td></tr> <tr><td>\1...\9</td><td>匹配第 n 个分组子表达式。</td></tr> <tr><td>\10</td><td>如果已匹配过，则匹配第 n 个分组子表达式。否则指向字符编码的八进制表示。</td></tr> </table> <br /> 

## 正则表达式实例

## 字符

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/ruby/</td><td>匹配 "ruby"</td></tr> <tr><td>&yen;</td><td>匹配 Yen 符号。Ruby 1.9 和 Ruby 1.8 支持多个字符。</td></tr> </table> 

## 字符类

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/[Rr]uby/ </td><td>匹配 "Ruby" 或 "ruby"</td></tr> <tr><td>/rub[ye]/ </td><td>匹配 "ruby" 或 "rube"</td></tr> <tr><td>/[aeiou]/</td><td>匹配任何一个小写元音字母</td></tr> <tr><td>/[0-9]/ </td><td>匹配任何一个数字，与 /[0123456789]/ 相同</td></tr> <tr><td>/[a-z]/</td><td>匹配任何一个小写 ASCII 字母</td></tr> <tr><td>/[A-Z]/</td><td>匹配任何一个大写 ASCII 字母</td></tr> <tr><td>/[a-zA-Z0-9]/</td><td>匹配任何一个括号内的字符</td></tr> <tr><td>/[^aeiou]/ </td><td>匹配任何一个非小写元音字母的字符</td></tr> <tr><td>/[^0-9]/</td><td>匹配任何一个非数字字符</td></tr> </table> 

## 特殊字符类

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/./ </td><td>匹配除了换行符以外的其他任意字符</td></tr> <tr><td>/./m </td><td>在多行模式下，也能匹配换行符</td></tr> <tr><td>/\d/</td><td>匹配一个数字，等同于 /[0-9]/</td></tr> <tr><td>/\D/ </td><td>匹配一个非数字，等同于 /[^0-9]/</td></tr> <tr><td>/\s/</td><td>匹配一个空白字符，等同于 /[ \t\r\n\f]/</td></tr> <tr><td>/\S/ </td><td>匹配一个非空白字符，等同于 /[^ \t\r\n\f]/</td></tr> <tr><td>/\w/ </td><td>匹配一个单词字符，等同于 /[A-Za-z0-9_]/</td></tr> <tr><td>/\W/</td><td>匹配一个非单词字符，等同于 /[^A-Za-z0-9_]/</td></tr> </table> 

## 重复

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/ruby?/ </td><td>匹配 "rub" 或 "ruby"。其中，y 是可有可无的。</td></tr> <tr><td>/ruby*/ </td><td>匹配 "rub" 加上 0 个或多个的 y。</td></tr> <tr><td>/ruby+/</td><td>匹配 "rub" 加上 1 个或多个的 y。</td></tr> <tr><td>/\d/</td><td>刚好匹配 3 个数字。</td></tr> <tr><td>/\d/</td><td>匹配 3 个或多个数字。</td></tr> <tr><td>/\d/</td><td>匹配 3 个、4 个或 5 个数字。</td></tr> </table> 

## 非贪婪重复

这会匹配最小次数的重复。

</p> <table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/&lt;.*&gt;/</td><td>贪婪重复：匹配 "&lt;ruby&gt;perl&gt;"</td></tr> <tr><td>/&lt;.*?&gt;/ </td><td>非贪婪重复：匹配 "&lt;ruby&gt;perl&gt;" 中的 "&lt;ruby&gt;"</td></tr> </table> 

## 通过圆括号进行分组 

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/\D\d+/ </td><td>无分组： + 重复 \d</td></tr> <tr><td>/(\D\d)+/ </td><td>分组： + 重复 \D\d 对</td></tr> <tr><td>/([Rr]uby(, )?)+/</td><td>匹配 "Ruby"、"Ruby, ruby, ruby"，等等</td></tr> </table> 

## 反向引用
这会再次匹配之前匹配过的分组。

</p> <table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/([Rr])uby&amp;\1ails/</td><td>匹配 ruby&amp;rails 或 Ruby&amp;Rails</td></tr> <tr><td> /(['"])(?:(?!\1).)*\1/</td><td>单引号或双引号字符串。\1 匹配第一个分组所匹配的字符，\2 匹配第二个分组所匹配的字符，依此类推。</td></tr> </table> 

## 替换

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/ruby|rube/</td><td>匹配 "ruby" 或 "rube"</td></tr> <tr><td>/rub(y|le))/</td><td>匹配 "ruby" 或 "ruble"</td></tr> <tr><td>/ruby(!+|\?)/ </td><td>"ruby" 后跟一个或多个 ! 或者跟一个 ?</td></tr> </table> 

## 锚 

这需要指定匹配位置。

</p> <table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/^Ruby/</td><td>匹配以 "Ruby" 开头的字符串或行</td></tr> <tr><td>/Ruby$/ </td><td>匹配以 "Ruby" 结尾的字符串或行</td></tr> <tr><td>/\ARuby/ </td><td>匹配以 "Ruby" 开头的字符串</td></tr> <tr><td>/Ruby\Z/</td><td>匹配以 "Ruby" 结尾的字符串</td></tr> <tr><td>/\bRuby\b/</td><td>匹配单词边界的 "Ruby"</td></tr> <tr><td>/\brub\B/</td><td>\B 是非单词边界：匹配 "rube" 和 "ruby" 中的 "rub"，但不匹配单独的 "rub"</td></tr> <tr><td>/Ruby(?=!)/</td><td>如果 "Ruby" 后跟着一个感叹号，则匹配 "Ruby"</td></tr> <tr><td>/Ruby(?!!)/ </td><td>如果 "Ruby" 后没有跟着一个感叹号，则匹配 "Ruby"</td></tr> </table> 

## 圆括号的特殊语法

<table > <tr><th style="width:25%">实例</th><th>描述</th></tr> <tr><td>/R(?#comment)/ </td><td>匹配 "R"。所有剩余的字符都是注释。</td></tr> <tr><td>/R(?i)uby/ </td><td>当匹配 "uby" 时不区分大小写。</td></tr> <tr><td>/R(?i:uby)/ </td><td>与上面相同。</td></tr> <tr><td>/rub(?:y|le))/</td><td>只分组，不进行 \1 反向引用</td></tr> </table>

## 搜索和替换

**sub** 和 **gsub** 及它们的替代变量 **sub!** 和 **gsub!** 是使用正则表达式时重要的字符串方法。

所有这些方法都是使用正则表达式模式执行搜索与替换操作。**sub** 和 **sub!** 替换模式的第一次出现，**gsub** 和 **gsub!** 替换模式的所有出现。

**sub** 和 **gsub** 返回一个新的字符串，保持原始的字符串不被修改，而 **sub!** 和 **gsub!** 则会修改它们调用的字符串。

下面是一个实例：

```
#!/usr/bin/ruby

phone = "2004-959-559 #This is Phone Number"

# 删除 Ruby 的注释
phone = phone.sub!(/#.*$/, "")   
puts "Phone Num : #{phone}"

# 移除数字以外的其他字符
phone = phone.gsub!(/\D/, "")    
puts "Phone Num : #{phone}"
```

这将产生以下结果：

```
Phone Num : 2004-959-559
Phone Num : 2004959559
```

下面是另一个实例：

```
#!/usr/bin/ruby

text = "rails are rails, really good Ruby on Rails"

# 把所有的 "rails" 改为 "Rails"
text.gsub!("rails", "Rails")

# 把所有的单词 "Rails" 都改成首字母大写
text.gsub!(/\brails\b/, "Rails")

puts "#{text}"
```

这将产生以下结果：

```
Rails are Rails, really good Ruby on Rails
```
