# Ruby 数组


Ruby 数组是任何对象的有序的、整数索引的集合。数组中的每个元素都与一个索引相关，并可通过索引进行获取。

数组的索引从 0 开始，这与 C 或 Java 中一样。一个负数的索引时相对于数组的末尾计数的，也就是说，索引为 -1 表示数组的最后一个元素，-2 表示数组中的倒数第二个元素，依此类推。

Ruby 数组可存储诸如 String、 Integer、 Fixnum、 Hash、 Symbol 等对象，甚至可以是其他 Array 对象。Ruby 数组不像其他语言中的数组那么刚性。当向数组添加元素时，Ruby 数组会自动增长。


## 创建数组

有多种方式创建或初始化数组。一种方式是通过 _new_ 类方法：

```
names = Array.new
```

您可以在创建数组的同时设置数组的大小：

```
names = Array.new(20)
```

数组 _names_ 的大小或长度为 20 个元素。您可以使用 size 或 length 方法返回数组的大小：

```
#!/usr/bin/ruby

names = Array.new(20)
puts names.size  # 返回 20
puts names.length # 返回 20
```

这将产生以下结果：

```
20
20
```

您可以给数组中的每个元素赋值，如下所示：

```
#!/usr/bin/ruby

names = Array.new(4, "mac")

puts "#{names}"
```

这将产生以下结果：

```
macmacmacmac
```

您也可以使用带有 new 的块，每个元素使用块中的计算结果来填充：

```
#!/usr/bin/ruby

nums = Array.new(10) { |e| e = e * 2 }

puts "#{nums}"
```

这将产生以下结果：

```
024681012141618
111


数组还有另一种方法，[]，如下所示：

```
nums = Array.[](1, 2, 3, 4,5)
```

数组创建的另一种形式如下所示：

```
nums = Array[1, 2, 3, 4,5]
```


在核心 Ruby 中可用的 _Kernel_ 模块有一个 Array 方法，只接受单个参数。在这里，该方法带有一个范围作为参数来创建一个数字数组：

```
#!/usr/bin/ruby

digits = Array(0..9)

puts "#{digits}"
```

这将产生以下结果：

```
0123456789
```

## 数组内建方法

我们需要有一个 Array 对象的实例来调用 Array 方法。下面是创建 Array 对象实例的方式：

```
Array.[](...) [or] Array[...] [or] [...]
```

这将返回一个使用给定对象进行填充的新的数组。现在，使用创建的对象，我们可以调用任意可用的实例方法。例如：

```
#!/usr/bin/ruby

digits = Array(0..9)

num = digits.at(6)

puts "#{num}"
```

这将产生以下结果：

```
6
```

下面是公共的数组方法（假设 _array_ 是一个 Array 对象）：

<table>
<tbody>
<tr>
<th style="width:5%">序号</th>

<th>方法 & 描述</th>

</tr>

<tr>
<td>1</td>

<td>**array & other_array**  
返回一个新的数组，包含两个数组中共同的元素，没有重复。</td>

</tr>

<tr>
<td>2</td>

<td>**array * int [or] array * str**  
返回一个新的数组，新数组通过连接 self 的 int 副本创建的。带有 String 参数时，相当于 self.join(str)。</td>

</tr>

<tr>
<td>3</td>

<td>**array + other_array**  
返回一个新的数组，新数组通过连接两个数组产生第三个数组创建的。</td>

</tr>

<tr>
<td>4</td>

<td>**array - other_array**  
返回一个新的数组，新数组是从初始数组中移除了在 other_array 中出现的项的副本。</td>

</tr>

<tr>
<td>5</td>

<td>**str <=> other_str**  
把 str 与 other_str 进行比较，返回 -1（小于）、0（等于）或 1（大于）。比较是区分大小写的。</td>

</tr>

<tr>
<td>6</td>

<td>**array | other_array**  
通过把 other_array 加入 array 中，移除重复项，返回一个新的数组。</td>

</tr>

<tr>
<td>7</td>

<td>**array << obj**  
把给定的对象附加到数组的末尾。该表达式返回数组本身，所以几个附加可以连在一起。</td>

</tr>

<tr>
<td>8</td>

<td>**array <=> other_array**  
如果数组小于、等于或大于 other_array，则返回一个整数（-1、 0 或 +1）。</td>

</tr>

<tr>
<td>9</td>

<td>**array == other_array**  
如果两个数组包含相同的元素个数，且每个元素与另一个数组中相对应的元素相等（根据 Object.==），那么这两个数组相等。</td>

</tr>

<tr>
<td>10</td>

<td>**array[index] [or] array[start, length] [or]  
 array[range] [or] array.slice(index) [or]  
 array.slice(start, length) [or] array.slice(range)**  
返回索引为 _index_ 的元素，或者返回从 _start_ 开始直至 _length_ 个元素的子数组，或者返回 _range_ 指定的子数组。负值索引从数组末尾开始计数（-1 是最后一个元素）。如果 _index_（或开始索引）超出范围，则返回 _nil_。</td>

</tr>

<tr>
<td>11</td>

<td>**array[index] = obj [or]  
 array[start, length] = obj or an_array or nil [or]  
 array[range] = obj or an_array or nil**  
设置索引为 _index_ 的元素，或者替换从 _start_ 开始直至 _length_ 个元素的子数组，或者替换 _range_ 指定的子数组。如果索引大于数组的当前容量，那么数组会自动增长。负值索引从数组末尾开始计数。如果 _length_ 为零则插入元素。如果在第二种或第三种形式中使用了 _nil_，则从 _self_ 删除元素。</td>

</tr>

<tr>
<td>12</td>

<td>**array.abbrev(pattern = nil)**  
为 _self_ 中的字符串计算明确的缩写集合。如果传递一个模式或一个字符串，只考虑当字符串匹配模式或者以该字符串开始时的情况。</td>

</tr>

<tr>
<td>13</td>

<td>**array.assoc(obj)**  
搜索一个数组，其元素也是数组，使用 obj.== 把 obj 与每个包含的数组的第一个元素进行比较。如果匹配则返回第一个包含的数组，如果未找到匹配则返回 _nil_。</td>

</tr>

<tr>
<td>14</td>

<td>**array.at(index)**  
返回索引为 index 的元素。一个负值索引从 _self_ 的末尾开始计数。如果索引超出范围则返回 nil。</td>

</tr>

<tr>
<td>15</td>

<td>**array.clear**  
从数组中移除所有的元素。</td>

</tr>

<tr>
<td>16</td>

<td>**array.collect { |item| block } [or]  
 array.map { |item| block }**  
为 _self_ 中的每个元素调用一次 _block_。创建一个新的数组，包含 block 返回的值。</td>

</tr>

<tr>
<td>17</td>

<td>**array.collect! { |item| block } [or]  
 array.map! { |item| block }**  
为 _self_ 中的每个元素调用一次 _block_，把元素替换为 _block_ 返回的值。</td>

</tr>

<tr>
<td>18</td>

<td>**array.compact**  
返回 _self_ 的副本，移除了所有的 _nil_ 元素。</td>

</tr>

<tr>
<td>19</td>

<td>**array.compact!**  
从数组中移除所有的 _nil_ 元素。如果没有变化则返回 _nil_。</td>

</tr>

<tr>
<td>20</td>

<td>**array.concat(other_array)**  
追加 other_array 中的元素到 _self_ 中。</td>

</tr>

<tr>
<td>21</td>

<td>**array.delete(obj) [or]   
array.delete(obj) { block }**  
从 _self_ 中删除等于 _obj_ 的项。如果未找到相等项，则返回 _nil_。如果未找到相等项且给出了可选的代码 _block_，则返回 _block_ 的结果。</td>

</tr>

<tr>
<td>22</td>

<td>**array.delete_at(index)**  
删除指定的 _index_ 处的元素，并返回该元素。如果 index 超出范围，则返回 _nil_。</td>

</tr>

<tr>
<td>23</td>

<td>**array.delete_if { |item| block }**  
当 _block_ 为 true 时，删除 _self_ 的每个元素。</td>

</tr>

<tr>
<td>24</td>

<td>**array.each { |item| block }**  
为 _self_ 中的每个元素调用一次 _block_，传递该元素作为参数。</td>

</tr>

<tr>
<td>25</td>

<td>**array.each_index { |index| block }**  
与 Array#each 相同，但是传递元素的 _index_，而不是传递元素本身。</td>

</tr>

<tr>
<td>26</td>

<td>**array.empty?**  
如果数组本身没有包含元素，则返回 true。</td>

</tr>

<tr>
<td>27</td>

<td>**array.eql?(other)**  
如果 _array_ 和 _other_ 是相同的对象，或者两个数组带有相同的内容，则返回 true。</td>

</tr>

<tr>
<td>28</td>

<td>**array.fetch(index) [or]   
array.fetch(index, default) [or]   
array.fetch(index) { |index| block }**  
尝试返回位置 _index_ 处的元素。如果 _index_ 位于数组外部，则第一种形式会抛出 _IndexError_ 异常，第二种形式会返回 _default_，第三种形式会返回调用 _block_ 传入 _index_ 的值。负值的 _index_ 从数组末尾开始计数。</td>

</tr>

<tr>
<td>29</td>

<td>**array.fill(obj) [or]  
 array.fill(obj, start [, length]) [or]  
 array.fill(obj, range) [or]  
 array.fill { |index| block } [or]  
 array.fill(start [, length] ) { |index| block } [or]  
 array.fill(range) { |index| block }**  
前面三种形式设置 _self_ 的被选元素为 _obj_。以 _nil_ 开头相当于零。_nil_ 的长度相当于 _self.length_。最后三种形式用 block 的值_填充_数组。_block_ 通过带有被填充的每个元素的绝对索引来传递。</td>

</tr>

<tr>
<td>30</td>

<td>**array.first [or]   
array.first(n)**  
返回数组的第一个元素或前 _n_ 个元素。如果数组为空，则第一种形式返回 _nil_，第二种形式返回一个空的数组。</td>

</tr>

<tr>
<td>31</td>

<td>**array.flatten**  
返回一个新的数组，新数组是一个一维的扁平化的数组（递归）。</td>

</tr>

<tr>
<td>32</td>

<td>**array.flatten!**  
把 _array_ 进行扁平化。如果没有变化则返回 _nil_。（数组不包含子数组。）</td>

</tr>

<tr>
<td>33</td>

<td>**array.frozen?**  
如果 _array_ 被冻结（或排序时暂时冻结），则返回 true。</td>

</tr>

<tr>
<td>34</td>

<td>**array.hash**  
计算数组的哈希代码。两个具有相同内容的数组将具有相同的哈希代码。</td>

</tr>

<tr>
<td>35</td>

<td>**array.include?(obj)**  
如果 _self_ 中包含 _obj_，则返回 true，否则返回 false。</td>

</tr>

<tr>
<td>36</td>

<td>**array.index(obj)**  
返回 _self_ 中第一个等于 obj 的对象的 _index_。如果未找到匹配则返回 _nil_。</td>

</tr>

<tr>
<td>37</td>

<td>**array.indexes(i1, i2, ... iN) [or]  
 array.indices(i1, i2, ... iN)**  
该方法在 Ruby 的最新版本中被废弃，所以请使用 Array#values_at。</td>

</tr>

<tr>
<td>38</td>

<td>**array.indices(i1, i2, ... iN) [or]  
 array.indexes(i1, i2, ... iN)**  
该方法在 Ruby 的最新版本中被废弃，所以请使用 Array#values_at。</td>

</tr>

<tr>
<td>39</td>

<td>**array.insert(index, obj...)**  
在给定的 _index_ 的元素前插入给定的值，index 可以是负值。</td>

</tr>

<tr>
<td>40</td>

<td>**array.inspect**  
创建一个数组的可打印版本。</td>

</tr>

<tr>
<td>41</td>

<td>**array.join(sep=$,)**  
返回一个字符串，通过把数组的每个元素转换为字符串，并使用 _sep_ 分隔进行创建的。</td>

</tr>

<tr>
<td>42</td>

<td>**array.last [or] array.last(n)**  
返回 _self_ 的最后一个元素。如果数组为_空_，则第一种形式返回 _nil_。</td>

</tr>

<tr>
<td>43</td>

<td>**array.length**  
返回 _self_ 中元素的个数。可能为零。</td>

</tr>

<tr>
<td>44</td>

<td>**array.map { |item| block } [or]  
 array.collect { |item| block }**  
为 _self_ 的每个元素调用一次 _block_。创建一个新的数组，包含 block 返回的值。</td>

</tr>

<tr>
<td>45</td>

<td>**array.map! { |item| block } [or]  
 array.collect! { |item| block }**  
为 _array_ 的每个元素调用一次 _block_，把元素替换为 block 返回的值。</td>

</tr>

<tr>
<td>46</td>

<td>**array.nitems**  
返回 _self_ 中 non-nil 元素的个数。可能为零。</td>

</tr>

<tr>
<td>47</td>

<td>**array.pack(aTemplateString)**  
根据 aTemplateString 中的指令，把数组的内容压缩为二进制序列。指令 A、 a 和 Z 后可以跟一个表示结果字段宽度的数字。剩余的指令也可以带有一个表示要转换的数组元素个数的数字。如果数字是一个星号（*），则所有剩余的数组元素都将被转换。任何指令后都可以跟一个下划线（_），表示指定类型使用底层平台的本地尺寸大小，否则使用独立于平台的一致的尺寸大小。在模板字符串中空格会被忽略。</td>

</tr>

<tr>
<td>48</td>

<td>**array.pop**  
从 _array_ 中移除最后一个元素，并返回该元素。如果 _array_ 为空则返回 _nil_。</td>

</tr>

<tr>
<td>49</td>

<td>**array.push(obj, ...)**  
把给定的 obj 附加到数组的末尾。该表达式返回数组本身，所以几个附加可以连在一起。</td>

</tr>

<tr>
<td>50</td>

<td>**array.rassoc(key)**  
搜索一个数组，其元素也是数组，使用 == 把 _key_ 与每个包含的数组的第二个元素进行比较。如果匹配则返回第一个包含的数组。</td>

</tr>

<tr>
<td>51</td>

<td>**array.reject { |item| block }**  
返回一个新的数组，包含当 block 不为 true 时的数组项。</td>

</tr>

<tr>
<td>52</td>

<td>**array.reject! { |item| block }**  
当 block 为真时，从 _array_ 删除元素，如果没有变化则返回 _nil_。相当于 Array#delete_if。</td>

</tr>

<tr>
<td>53</td>

<td>**array.replace(other_array)**  
把 _array_ 的内容替换为 _other_array_ 的内容，必要的时候进行截断或扩充。</td>

</tr>

<tr>
<td>54</td>

<td>**array.reverse**  
返回一个新的数组，包含倒序排列的数组元素。</td>

</tr>

<tr>
<td>55</td>

<td>**array.reverse!**  
把 _array_ 进行逆转。</td>

</tr>

<tr>
<td>56</td>

<td>**array.reverse_each {|item| block }**  
与 Array#each 相同，但是把 _array_ 进行逆转。</td>

</tr>

<tr>
<td>57</td>

<td>**array.rindex(obj)**  
返回 array 中最后一个等于 obj 的对象的索引。如果未找到匹配，则返回 _nil_。</td>

</tr>

<tr>
<td>58</td>

<td>**array.select {|item| block }**  
调用从数组传入连续元素的 block，返回一个数组，包含 block 返回 _true_ 值时的元素。</td>

</tr>

<tr>
<td>59</td>

<td>**array.shift**  
返回 _self_ 的第一个元素，并移除该元素（把所有的其他元素下移一位）。如果数组为空，则返回 _nil_。</td>

</tr>

<tr>
<td>60</td>

<td>**array.size**  
返回 _array_ 的长度（元素的个数）。length 的别名。</td>

</tr>

<tr>
<td>61</td>

<td>**array.slice(index) [or] array.slice(start, length) [or]  
 array.slice(range) [or] array[index] [or]  
 array[start, length] [or] array[range]**  
返回索引为 _index_ 的元素，或者返回从 _start_ 开始直至 _length_ 个元素的子数组，或者返回 _range_ 指定的子数组。负值索引从数组末尾开始计数（-1 是最后一个元素）。如果 _index_（或开始索引）超出范围，则返回 _nil_。</td>

</tr>

<tr>
<td>62</td>

<td>**array.slice!(index) [or] array.slice!(start, length) [or]  
 array.slice!(range)**  
删除 _index_（长度是可选的）或 _range_ 指定的元素。返回被删除的对象、子数组，如果 _index_ 超出范围，则返回 _nil_。</td>

</tr>

<tr>
<td>63</td>

<td>**array.sort [or] array.sort { | a,b | block }**  
返回一个排序的数组。</td>

</tr>

<tr>
<td>64</td>

<td>**array.sort! [or] array.sort! { | a,b | block }**  
把数组进行排序。</td>

</tr>

<tr>
<td>65</td>

<td>**array.to_a**  
返回 _self_。如果在 _Array_ 的子类上调用，则把接收参数转换为一个 Array 对象。</td>

</tr>

<tr>
<td>66</td>

<td>**array.to_ary**  
返回 self。</td>

</tr>

<tr>
<td>67</td>

<td>**array.to_s**  
返回 self.join。</td>

</tr>

<tr>
<td>68</td>

<td>**array.transpose**  
假设 self 是数组的数组，且置换行和列。</td>

</tr>

<tr>
<td>69</td>

<td>**array.uniq**  
返回一个新的数组，移除了 _array_ 中的重复值。</td>

</tr>

<tr>
<td>70</td>

<td>**array.uniq!**  
从 _self_ 中移除重复元素。如果没有变化（也就是说，未找到重复），则返回 _nil_。</td>

</tr>

<tr>
<td>71</td>

<td>**array.unshift(obj, ...)**  
把对象前置在数组的前面，其他元素上移一位。</td>

</tr>

<tr>
<td>72</td>

<td>**array.values_at(selector,...)**  
返回一个数组，包含 self 中与给定的 _selector_（一个或多个）相对应的元素。选择器可以是整数索引或者范围。</td>

</tr>

<tr>
<td>73</td>

<td>**array.zip(arg, ...) [or]   
array.zip(arg, ...){ | arr | block }**  
把任何参数转换为数组，然后把 _array_ 的元素与每个参数中相对应的元素合并。</td>

</tr>

</tbody>

</table>

## 数组 pack 指令

下表列出了方法 Array#pack 的压缩指令。

</p> <table > <tr><th style="width:25%">指令</th><th>描述</th></tr> <tr><td>@</td><td>移动到绝对位置。</td></tr> <tr><td>A</td><td>ASCII 字符串（填充 space，count 是宽度）。</td></tr> <tr><td>a</td><td>ASCII 字符串（填充 null，count 是宽度）。</td></tr> <tr><td>B</td><td>位字符串（降序）</td></tr> <tr><td>b</td><td>位字符串（升序）。</td></tr> <tr><td>C</td><td>无符号字符。</td></tr> <tr><td>c</td><td>字符。</td></tr> <tr><td>D, d</td><td>双精度浮点数，原生格式。</td></tr> <tr><td>E</td><td>双精度浮点数，little-endian 字节顺序。</td></tr> <tr><td>e</td><td>单精度浮点数，little-endian 字节顺序。</td></tr> <tr><td>F, f</td><td>单精度浮点数，原生格式。</td></tr> <tr><td>G</td><td>双精度浮点数，network（big-endian）字节顺序。</td></tr> <tr><td>g</td><td>单精度浮点数，network（big-endian）字节顺序。</td></tr> <tr><td>H</td><td>十六进制字符串（高位优先）。</td></tr> <tr><td>h</td><td>十六进制字符串（低位优先）。</td></tr> <tr><td>I</td><td>无符号整数。</td></tr> <tr><td>i</td><td>整数。</td></tr> <tr><td>L</td><td>无符号 long。</td></tr> <tr><td>l</td><td>Long。</td></tr> <tr><td>M</td><td>引用可打印的，MIME 编码。</td></tr> <tr><td>m</td><td>Base64 编码字符串。</td></tr> <tr><td>N</td><td>Long，network（big-endian）字节顺序。</td></tr> <tr><td>n</td><td>Short，network（big-endian）字节顺序。</td></tr> <tr><td>P</td><td>指向一个结构（固定长度的字符串）。</td></tr> <tr><td>p</td><td>指向一个空结束字符串。</td></tr> <tr><td>Q, q</td><td>64 位数字。</td></tr> <tr><td>S</td><td>无符号 short。</td></tr> <tr><td>s</td><td>Short。</td></tr> <tr><td>U</td><td>UTF-8。</td></tr> <tr><td>u</td><td>UU 编码字符串。</td></tr> <tr><td>V</td><td>Long，little-endian 字节顺序。</td></tr> <tr><td>v</td><td>Short，little-endian 字节顺序。</td></tr> <tr><td>w</td><td>BER 压缩的整数 \fnm。</td></tr> <tr><td>X</td><td>向后跳过一个字节。</td></tr> <tr><td>x</td><td>Null 字节。</td></tr> <tr><td>Z</td><td>与 a 相同，除了 null 会被加上 *。</td></tr> </table> 

## 实例

尝试下面的实例，压缩各种数据。

```
a = [ "a", "b", "c" ]
n = [ 65, 66, 67 ]
puts a.pack("A3A3A3")   #=> "a  b  c  "
puts a.pack("a3a3a3")   #=> "a\000\000b\000\000c\000\000"
puts n.pack("ccc")      #=> "ABC"
```

这将产生以下结果：

```
a  b  c
abc
ABC
```
