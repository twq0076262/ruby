# Ruby 发送邮件 – SMTP

SMTP（Simple Mail Transfer Protocol）即简单邮件传输协议,它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。

Ruby提供了 Net::SMTP 来发送邮件，并提供了两个方法 new 和 start:

* **new** 方法有两个参数：
    * _server name_ 默认为 localhost
    * _port number_ 默认为 25
* **start** 方法有以下参数：
    * _server_ \- SMTP 服务器 IP, 默认为 localhost
    * _port_ \- 端口号，默认为 25
    * _domain_ \- 邮件发送者域名，默认为 ENV["HOSTNAME"]
    * _account_ \- 用户名，默认为 nil
    * _password_ \- 用户密码，默认为nil
    * _authtype_ \- 验证类型，默认为 _cram_md5_

SMTP 对象实例化方法调用了 sendmail, 参数如下：

* _source_ \- 一个字符串或数组或每个迭代器在任一时间中返回的任何东西。
* _sender_ -一个字符串，出现在 email 的表单字段。
* _recipients_ \- 一个字符串或字符串数组，表示收件人的地址。

### 实例

以下提供了简单的Ruby脚本来发送邮件:

```
    require 'net/smtp'

    message = <
    To: A Test User 
    Subject: SMTP e-mail test

    This is a test e-mail message.
    MESSAGE_END

    Net::SMTP.start('localhost') do |smtp|
      smtp.send_message message, 'me@fromdomain.com',
                                 'test@todomain.com'
    end
```

在以上实例中，你已经设置了一个基本的电子邮件消息，注意正确的标题格式。一个电子邮件要要From，To和Subject，文本内容与头部信息间需要一个空行。

使用Net::SMTP连接到本地机器上的SMTP服务器，使用send_message方法来发送邮件，方法参数为发送者邮件与接收者邮件。

如果你没有运行在本机上的SMTP服务器，您可以使用Net::SMTP与远程SMTP服务器进行通信。如果使用网络邮件服务（如Hotmail或雅虎邮件），您的电子邮件提供者会为您提供发送邮件服务器的详细信息:

```
    Net::SMTP.start('mail.your-domain.com')
```

以上代码将连接主机为 mail.your-domain.com，端口号为 25的邮件服务器，如果需要填写用户名密码，则代码如下：

```
    Net::SMTP.start('mail.your-domain.com',
                    25,
                    'localhost',
                    'username', 'password' :plain)
```

以上实例使用了指定的用户名密码连接到主机为 mail.your-domain.com，端口号为 25的邮件服务器。


## 使用 Ruby 发送 HTML 邮件

Net::SMTP同样提供了支持发送 HTML 格式的邮件。

发送电子邮件时你可以设置MIME版本，文档类型，字符集来发送HTML格式的邮件。

### 实例

以下实例用于发送 HTML 格式的邮件：

```
    require 'net/smtp'

    message = <
    To: A Test User 
    MIME-Version: 1.0
    Content-type: text/html
    Subject: SMTP e-mail test

    This is an e-mail message to be sent in HTML format

    This is HTML message.
    
This is headline.


    MESSAGE_END

    Net::SMTP.start('localhost') do |smtp|
      smtp.send_message message, 'me@fromdomain.com',
                                 'test@todomain.com'
    end

```


## 发送带附件的邮件

如果需要发送混合内容的电子邮件，需要设置Content-type为multipart/mixed。 这样就可以在邮件中添加附件内容。

附件在传输前需要使用 **pack("m")** 函数将其内容转为 base64 格式。

### 实例

以下实例将发送附件为 /tmp/test.txt 的邮件：

```
    require 'net/smtp'

    filename = "/tmp/test.txt"
    # 读取文件并编码为base64格式
    filecontent = File.read(filename)
    encodedcontent = [filecontent].pack("m")   # base64

    marker = "AUNIQUEMARKER"

    body =<
    To: A Test User 
    Subject: Sending Attachement
    MIME-Version: 1.0
    Content-Type: multipart/mixed; boundary=#{marker}
    --#{marker}
    EOF

    # 定义消息动作
    part2 =< e
      print "Exception occured: " + e
    end
```

**注意：**你可以指定多个发送的地址，但需要使用逗号隔开。 