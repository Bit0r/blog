## 问题
有一个email的报文如下，请分析这个email报文
```smtp
Received: from 65.54.246.203 (EHLO bay0-omc3-s3.bay0.hotmail.com) (65.54.246.203) by mta419.mail.mud.yahoo.com with SMTP; Sat, 19 May 2007 16:53:51 -0700
Received: from hotmail.com ([65.55.135.106]) by bay0-omc3-s3.bay0.hotmail.com with Microsoft SMTPSVC(6.0.3790.2668); Sat, 19 May 2007 16:52:42 -0700
Received: from mail pickup service by hotmail.com with Microsoft SMTPSVC; Sat, 19 May 2007 16:52:41 -0700
Message-ID: <BAY130-F26D9E35BF59E0D18A819AFB9310@phx.gbl>
Received: from 65.55.135.123 by by130fd.bay130.hotmail.msn.com with HTTP; Sat, 19 May 2007 23:52:36 GMT
From: "prithula dhungel" <prithuladhungel@hotmail.com>
To: prithula@yahoo.com
Bcc:
Subject: Test mail
Date: Sat, 19 May 2007 23:52:36 +0000
Mime-Version: 1.0
Content-Type: Text/html; format=flowed
Return-Path: prithuladhungel@hotmail.com
```

## 分析

* `Received:` 此标头字段指示SMTP服务器发送和接收邮件消息的顺序，包括相应的时间戳。在此示例中，有4条“已接收: ”标题行。也就是说，邮件先通过5个不同的SMTP服务器传递，然后再传递到收件人的邮箱。\
第四个`Received:`标头指示从发件人的SMTP服务器到邮件服务器链中第二个SMTP服务器的邮件流。发件人的SMTP服务器位于地址`65.55.135.123`，链中的第二个SMTP服务器为`by130fd.bay130.hotmail.msn.com`。\
第三个`Received:`标头指示从链中第二个SMTP服务器到第三台服务器的邮件流，依此类推。\
第一个`Received:`标头表示链中从第四个SMTP服务器到最后一个SMTP服务器（即接收者的邮件服务器）的邮件流。
* `Message-ID:` 消息的ID为`BAY130-F26D9E35BF59E0D18A819AFB9310@phx.gbl`（由`bay0-omc3-s3.bay0.hotmail.com`设置）。`Message-ID`是邮件系统在首次创建邮件时分配的唯一字符串
* `From:` 这表示邮件发件人的电子邮件地址。在给定的示例中，发件人为`prithuladhungel@hotmail.com`
* `To:` 此字段指示邮件收件人的电子邮件地址。在示例中，接收者是`prithula@yahoo.com`
* `Subject:` 这给出了邮件的主题（如果发件人指定了任何主题）。在此示例中，发件人指定的主题是`Test mail`
* `Data:` 发件人发送邮件的日期和时间。在此示例中，发件人于格林尼治标准时间2007年5月19日发送邮件。
* `Mime-version:` 用于邮件的MIME版本。在示例中，它是1.0。
* `Content-type:` 邮件正文中内容的类型。在示例中，它是`text/html`。
* `Return-Path:` 如果此邮件的收件人希望回复发件人，则指定将邮件发送到的电子邮件地址。发件人的邮件服务器也使用它来退回无法投递的邮件。在示例中，返回地址为`prithuladhungel@hotmail.com`。