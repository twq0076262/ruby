# Ruby 哈希（Hash）


哈希（Hash）是类似 "employee" => "salary" 这样的键值对的集合。哈希的索引是通过任何对象类型的任意键来完成的，而不是一个整数索引，其他与数组相似。

通过键或值遍历哈希的顺序看起来是随意的，且通常不是按照插入顺序。如果您尝试通过一个不存在的键访问哈希，则方法会返回 _nil_。

与数组一样，有各种不同的方式来创建哈希。您可以通过 _new_ 类方法创建一个空的哈希：

```
    months = Hash.new
```

您也可以使用 _new_ 创建带有默认值的哈希，不带默认值的哈希是 _nil_：

```
    months = Hash.new( "month" )

    or

    months = Hash.new "month"
```

当您访问带有默认值的哈希中的任意键时，如果键或值不存在，访问哈希将返回默认值：

```
    #!/usr/bin/ruby

    months = Hash.new( "month" )

    puts "#{months[0]}"
    puts "#{months[72]}"
```

这将产生以下结果：

```
    month
    month

    #!/usr/bin/ruby

    H = Hash["a" => 100, "b" => 200]

    puts "#{H['a']}"
    puts "#{H['b']}"
```

这将产生以下结果：

```
    100
    200
```

您可以使用任何的 Ruby 对象作为键或值，甚至可以使用数组，所以下面的实例是一个有效的实例：

```
    [1,"jan"] => "January"
```

我们需要有一个 Hash 对象的实例来调用 Hash 方法。下面是创建 Hash 对象实例的方式：

```
    Hash[[key =>|, value]* ] or

    Hash.new [or] Hash.new(obj) [or]

    Hash.new { |hash, key| block }
```

这将返回一个使用给定对象进行填充的新的哈希。现在，使用创建的对象，我们可以调用任意可用的实例方法。例如：

```
    #!/usr/bin/ruby

    $, = ", "
    months = Hash.new( "month" )

    months = {"1" => "January", "2" => "February"}

    keys = months.keys

    puts "#{keys}"
```

这将产生以下结果：

```
    2, 1
```

下面是公共的哈希方法（假设 _hash_ 是一个 Hash 对象）：

</p> <table > <tr><th style="width:5%">序号</th><th>方法 & 描述</th></tr> <tr><td>1</td><td><b>hash == other_hash</b><br />检查两个哈希是否具有相同的键值对个数，键值对是否相互匹配，来判断两个哈希是否相等。</td></tr> <tr><td>2</td><td><b>hash.[key]</b><br />使用键，从哈希引用值。如果未找到键，则返回默认值。</td></tr> <tr><td>3</td><td><b>hash.[key]=value</b><br />把 <i>value</i> 给定的值与 <i>key</i> 给定的键进行关联。</td></tr> <tr><td>4</td><td><b>hash.clear</b><br />从哈希中移除所有的键值对。</td></tr> <tr><td>5</td><td><b>hash.default(key = nil)</b><br />返回 <i>hash</i> 的默认值，如果未通过 default= 进行设置，则返回 nil。（如果键在 <i>hash</i> 中不存在，则 [] 返回一个默认值。）</td></tr> <tr><td>6</td><td><b>hash.default = obj</b><br />为 <i>hash</i> 设置默认值。</td></tr> <tr><td>7</td><td><b>hash.default_proc</b><br />如果 <i>hash</i> 通过块来创建，则返回块。</td></tr> <tr><td>8</td><td><b>hash.delete(key) [or]<br /> array.delete(key) { |key| block }</b><br />通过 <i>key</i> 从 <i>hash</i> 中删除键值对。如果使用了块 且未找到匹配的键值对，则返回块的结果。把它与 <i>delete_if</i> 进行比较。</td></tr> <tr><td>9</td><td><b>hash.delete_if { |key,value| block }</b><br />为 block 为 <i>true</i> 的每个块，从 <i>hash</i> 中删除键值对。</td></tr> <tr><td>10</td><td><b>hash.each { |key,value| block }</b><br />遍历 <i>hash</i>，为每个 <i>key</i> 调用一次 block，传递 key-value 作为一个二元素数组。</td></tr> <tr><td>11</td><td><b>hash.each_key { |key| block }</b><br />遍历 <i>hash</i>，为每个 <i>key</i> 调用一次 block，传递 <i>key</i> 作为参数。</td></tr> <tr><td>12</td><td><b>hash.each_key { |key_value_array| block }</b><br />遍历 <i>hash</i>，为每个 <i>key</i> 调用一次 block，传递 <i>key</i> 和 <i>value</i> 作为参数。</td></tr> <tr><td>13</td><td><b>hash.each_key { |value| block }</b><br />遍历 <i>hash</i>，为每个 <i>key</i> 调用一次 block，传递 <i>value</i> 作为参数。</td></tr> <tr><td>14</td><td><b>hash.empty?</b><br />检查 hash 是否为空（不包含键值对），返回 <i>true</i> 或 <i>false</i>。</td></tr> <tr><td>15</td><td><b>hash.fetch(key [, default] ) [or]<br /> hash.fetch(key) { | key | block }</b><br />通过给定的 <i>key</i> 从 <i>hash</i> 返回值。如果未找到 <i>key</i>，且未提供其他参数，则抛出 <i>IndexError</i> 异常；如果给出了 <i>default</i>，则返回 <i>default</i>；如果指定了可选的 block，则返回 block 的结果。</td></tr> <tr><td>16</td><td><b>hash.has_key?(key) [or] hash.include?(key) [or]<br /> hash.key?(key) [or] hash.member?(key)</b><br />检查给定的 <i>key</i> 是否存在于哈希中，返回 <i>true</i> 或 <i>false</i>。</td></tr> <tr><td>17</td><td><b>hash.has_value?(value)</b><br />检查哈希是否包含给定的 <i>value</i>。</td></tr> <tr><td>18</td><td><b>hash.index(value)</b><br />为给定的 <i>value</i> 返回哈希中的 <i>key</i>，如果未找到匹配值则返回 <i>nil</i>。</td></tr> <tr><td>19</td><td><b>hash.indexes(keys)</b><br />返回一个新的数组，由给定的键的值组成。找不到的键将插入默认值。该方法已被废弃，请使用 select。</td></tr> <tr><td>20</td><td><b>hash.indices(keys)</b><br />返回一个新的数组，由给定的键的值组成。找不到的键将插入默认值。该方法已被废弃，请使用 select。</td></tr> <tr><td>21</td><td><b>hash.inspect</b><br />返回哈希的打印字符串版本。</td></tr> <tr><td>22</td><td><b>hash.invert</b><br />创建一个新的 <i>hash</i>，倒置 <i>hash</i> 中的 <i>keys</i> 和 <i>values</i>。也就是说，在新的哈希中，<i>hash</i> 中的键将变成值，值将变成键。</td></tr> <tr><td>23</td><td><b>hash.keys</b><br />创建一个新的数组，带有 <i>hash</i> 中的键。/td></td></tr> <tr><td>24</td><td><b>hash.length</b><br />以整数形式返回 <i>hash</i> 的大小或长度。</td></tr> <tr><td>25</td><td><b>hash.merge(other_hash) [or]<br /> hash.merge(other_hash) { |key, oldval, newval| block }</b><br />返回一个新的哈希，包含 <i>hash</i> 和 <i>other_hash</i> 的内容，重写 hash 中与 <i>other_hash</i> 带有重复键的键值对。</td></tr> <tr><td>26</td><td><b>hash.merge!(other_hash) [or]<br /> hash.merge!(other_hash) { |key, oldval, newval| block }</b><br />与 merge 相同，但实际上 hash 发生了变化。</td></tr> <tr><td>27</td><td><b>hash.rehash</b><br />基于每个 <i>key</i> 的当前值重新建立 <i>hash</i>。如果插入后值发生了改变，该方法会重新索引 <i>hash</i>。</td></tr> <tr><td>28</td><td><b>hash.reject { |key, value| block }</b><br />为 <i>block</i> 为 <i>true</i> 的每个键值对创建一个新的 <i>hash</i>。</td></tr> <tr><td>29</td><td><b>hash.reject! { |key, value| block }</b><br />与 <i>reject</i> 相同，但实际上 hash 发生了变化。</td></tr> <tr><td>30</td><td><b>hash.replace(other_hash)</b><br />把 <i>hash</i> 的内容替换为 <i>other_hash</i> 的内容。</td></tr> <tr><td>31</td><td><b>hash.select { |key, value| block }</b><br />返回一个新的数组，由 <i>block</i> 返回 <i>true</i> 的 <i>hash</i> 中的键值对组成。</td></tr> <tr><td>32</td><td><b>hash.shift</b><br />从 <i>hash</i> 中移除一个键值对，并把该键值对作为二元素数组返回。</td></tr> <tr><td>33</td><td><b>hash.size</b><br />以整数形式返回 <i>hash</i> 的 <i>size</i> 或 length。</td></tr> <tr><td>34</td><td><b>hash.sort</b><br />把 <i>hash</i> 转换为一个包含键值对数组的二维数组，然后进行排序。</td></tr> <tr><td>35</td><td><b>hash.store(key, value)</b><br />存储 <i>hash</i> 中的一个键值对。</td></tr> <tr><td>36</td><td><b>hash.to_a</b><br />从 hash 中创建一个二维数组。每个键值对转换为一个数组，所有这些数组都存储在一个数组中。</td></tr> <tr><td>37</td><td><b>hash.to_hash</b><br />返回 <i>hash</i>（self）。</td></tr> <tr><td>38</td><td><b>hash.to_s</b><br />把 <i>hash</i> 转换为一个数组，然后把该数组转换为一个字符串。</td></tr> <tr><td>39</td><td><b>hash.update(other_hash) [or]<br /> hash.update(other_hash) {|key, oldval, newval| block}</b><br />返回一个新的哈希，包含 <i>hash</i> 和 <i>other_hash</i> 的内容，重写 <i>hash</i> 中与 <i>other_hash</i> 带有重复键的键值对。</td></tr> <tr><td>40</td><td><b>hash.value?(value)</b><br />检查 <i>hash</i> 是否包含给定的 <i>value</i>。</td></tr> <tr><td>41</td><td><b>hash.values</b><br />返回一个新的数组，包含 <i>hash</i> 的所有值。</td></tr> <tr><td>42</td><td><b>hash.values_at(obj, ...)</b><br />返回一个新的数组，包含 <i>hash</i> 中与给定的键相关的值。</td></tr> </table> 