# Ruby CGI方法

以下为CGI类的方法列表：

</p> <table > <tbody><tr><th style="width:5%">序号</th><th>方法描述</th></tr> <tr><td>1</td><td><b>CGI::new([ level="query"])</b><br />创建 CGI 对象。query可以是以下值: <ul > <li><p><b>query:</b> 没有 HTML 生成输出</p></li> <li><p><b>html3:</b> HTML3.2</p></li> <li><p><b>html4:</b> HTML4.0 Strict</p></li> <li><p><b>html4Tr:</b> HTML4.0 Transitional</p></li> <li><p><b>html4Fr:</b> HTML4.0 Frameset</p></li> </ul> </td></tr> <tr><td>2</td><td><b>CGI::escape( str)</b><br />使用 URL 编码来转义字符串</td></tr> <tr><td>3</td><td><b>CGI::unescape( str)</b><br />对通过 escape() 编码的字符串进行解码。</td></tr> <tr><td>4</td><td><b>CGI::escapeHTML( str)</b><br />编码 HTML 特殊字符, 包括: &amp; &lt; &gt;。</td></tr> <tr><td>5</td><td><b>CGI::unescapeHTML( str)</b><br />解码 HTML 特殊字符, 包括: &amp; &lt; &gt;。</td></tr> <tr><td>6</td><td><b>CGI::escapeElement( str[, element...])</b><br />在指定的 HTML 元素中编码 HTML 特殊字符。</td></tr> <tr><td>7</td><td><b>CGI::unescapeElement( str, element[, element...])</b><br />在指定的 HTML 元素中解码 HTML 特殊字符。</td></tr> <tr><td>8</td><td><b>CGI::parse( query)</b><br />解析查询字符串，并返回包含哈希的 键=》值 对。</td></tr> <tr><td>9</td><td><b>CGI::pretty( string[, leader=" "])</b><br />返回整齐的HTML格式。 如果指定了 <i>leader</i> ，它将写入到每一行的开头。 <i>leader</i> 默认值为两个空格。</td></tr> <tr><td>10</td><td><b>CGI::rfc1123_date( time)</b><br />根据 RFC-1123 来格式化时间 (例如, Tue, 2 Jun 2008 00:00:00 GMT)。</td></tr> </tbody></table> <hr />

## CGI 实例化方法

以下实例中我们将 CGI::new 的对象赋值给 c 变量，方法列表如下：

</p> <table > <tbody><tr><th style="width:5%">序号</th><th>方法描述</th></tr> <tr><td>1</td><td><b>c[ name]</b><br />返回一个数组，包含了对应字段名为 <i>name</i> 的值。</td></tr> <tr><td>2</td><td><b>c.checkbox( name[, value[, check=false]])<br /> c.checkbox( options)</b><br />返回 HTML 字符串用于定义 checkbox 字段。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>3</td><td><b>c.checkbox_group( name, value...)<br /> c.checkbox_group( options)</b><br />>返回 HTML 字符串用于定义 checkbox 组。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>4</td><td><b>c.file_field( name[, size=20[, max]])<br /> c.file_field( options)</b><br />返回定义 file 字段的HTML字符串。</td></tr> <tr><td>5</td><td><b>c.form([ method="post"[, url]]) { ...}<br /> c.form( options)</b><br />返回定义 form 表单的HTML字符串。 如果指定了代码块，将作为表单内容输出。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>6</td><td><b>c.cookies</b><br />返回 CGI::Cookie 对象，包含了cookie 中的键值对。</td></tr> <tr><td>7</td><td><b>c.header([ header])</b><br />返回 CGI 头部的信息。如果 header 参数是哈希值，其键 - 值对，用于创建头部信息。</td></tr> <tr><td>8</td><td><b>c.hidden( name[, value])<br /> c.hidden( options)</b><br />返回定义一个隐藏字段的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>9</td><td><b>c.image_button( url[, name[, alt]])<br /> c.image_button( options)</b><br />返回定义一个图像按钮的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>10</td><td><b>c.keys</b><br />返回一个数组，包含了表单的字段名。</td></tr> <tr><td>11</td><td><b>c.key?( name)<br /> c.has_key?( name)<br /> c.include?( name)</b><br />如果表单包含了指定的字段名返回 true。</td></tr> <tr><td>12</td><td><b>c.multipart_form([ url[, encode]]) { ...}<br /> c.multipart_form( options) { ...}</b><br />返回定义一个多媒体表单（multipart）的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>13</td><td><b>c.out([ header]) { ...}</b><br />生成 HTML 并输出。使用由块的输出来创建页面的主体生成的字符串。</td></tr> <tr><td>14</td><td><b>c.params</b><br />返回包含表单字段名称和值的哈希值。</td></tr> <tr><td>15</td><td><b>c.params= hash</b><br />设置使用字段名和值。</td></tr> <tr><td>16</td><td><b>c.password_field( name[, value[, size=40[, max]]])<br /> c.password_field( options)</b><br />返回定义一个password字段的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>17</td><td><b>c.popup_menu( name, value...)<br /> c.popup_menu( options)<br /> c.scrolling_list( name, value...)<br /> c.scrolling_list( options)</b><br />返回定义一个弹出式菜单的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>18</td><td><b>c.radio_button( name[, value[, checked=false]])<br /> c.radio_button( options)</b><br />返回定义一个radio字段的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>19</td><td><b>c.radio_group( name, value...)<br /> c.radio_group( options)</b><br />返回定义一个radio按钮组的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>20</td><td><b>c.reset( name[, value])<br /> c.reset( options)</b><br />返回定义一个reset按钮的HTML字符串。 标签的属性可以以一个哈希函数作为参数传递</td></tr> <tr><td>21</td><td><b>c.text_field( name[, value[, size=40[, max]]])<br /> c.text_field( options)</b><br />返回定义一个text字段的HTML字符串。标签的属性可以以一个哈希函数作为参数传递。</td></tr> <tr><td>22</td><td><b>c.textarea( name[, cols=70[, rows=10]]) { ...}<br /> c.textarea( options) { ...}</b><br />返回定义一个textarea字段的HTML字符串。 如果指定了块，代码块输出的字符串将作为 textarea 的内容。 标签的属性可以以一个哈希函数作为参数传递。</td></tr> </tbody></table> <hr /> 

## HTML 生成方法

你可以再 CGI 实例中使用相应的 HTML 标签名来创建 HTML 标签，实例如下：

```
#!/usr/bin/ruby

require "cgi"
cgi = CGI.new("html4")
cgi.out{
   cgi.html{
      cgi.head{ "\n"+cgi.title{"This Is a Test"} } +
      cgi.body{ "\n"+
         cgi.form{"\n"+
            cgi.hr +
            cgi.h1 { "A Form: " } + "\n"+
            cgi.textarea("get_text") +"\n"+
            cgi.br +
            cgi.submit
         }
      }
   }
}
```

## CGI 对象属性

你可以再 CGI 实例中使用以下属性：

</p> <table > <tbody><tr><th style="width:50%">属性</th><th>返回值</th></tr> <tr><td>accept</td><td>可接受的 MIME 类型</td></tr> <tr><td>accept_charset</td><td>可接受的字符集</td></tr> <tr><td>accept_encoding</td><td>可接受的编码</td></tr> <tr><td>accept_language</td><td>可接受的语言</td></tr> <tr><td>auth_type</td><td>可接受的类型</td></tr> <tr><td>raw_cookie</td><td>Cookie 数据 (原字符串)</td></tr> <tr><td>content_length</td><td>内容长度（Content length）</td></tr> <tr><td>content_type</td><td>内容类型（Content type）</td></tr> <tr><td>From</td><td>Client e-mail 地址</td></tr> <tr><td>gateway_interface</td><td>CGI 版本</td></tr> <tr><td>path_info</td><td>路径</td></tr> <tr><td>path_translated</td><td>转换后的路径</td></tr> <tr><td>Query_string</td><td>查询字符串</td></tr> <tr><td>referer</td><td>之前访问网址</td></tr> <tr><td>remote_addr</td><td>客户端主机地址(IP)</td></tr> <tr><td>remote_host</td><td>客户端主机名</td></tr> <tr><td>remote_ident</td><td>客户端名</td></tr> <tr><td>remote_user</td><td>经过身份验证的用户</td></tr> <tr><td>request_method</td><td> 请求方法(GET, POST, 等。)</td></tr> <tr><td>script_name</td><td>参数名 </td></tr> <tr><td>server_name</td><td>服务器名</td></tr> <tr><td>server_port</td><td>服务器端口</td></tr> <tr><td>server_protocol</td><td>服务器协议</td></tr> <tr><td>server_software</td><td>服务器软件</td></tr> <tr><td>user_agent</td><td>用户代理（User agent）</td></tr> </tbody></table> 