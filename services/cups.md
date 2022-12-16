# 配置网络打印服务

## 服务器端

确保用户在`lpadmin`组内，这样才可以管理打印机。

### GUI方式

1. 在设置->打印机中添加打印机，然后配置好驱动

2. 在系统首选项中勾选“共享连接到此系统的打印机”，
如果还想要在非局域网中远程打印则勾选“允许来自互联网的打印机请求”（不推荐）

3. 选择要共享的打印机，勾选“共享此打印机”

![GUI](../img/services/cups/gui.avif)

### WebUI方式

1. 进行端口转发

```bash
ssh -L 6310:localhost:631 <remotehost>
```

2. 打开浏览器，访问<http://localhost:6310>

3. 在“Administration”中勾选“Share printers connected to this system”

4. 如果还想要在非局域网中远程打印则勾选“Allow printing from the Internet”（不推荐）

5. 如果想要不进行端口转发，直接远程管理打印机，则勾选“Allow remote administration”

![Administration](../img/services/cups/admin.avif)

6. 在“Printers”中点击要管理的打印机，如果没有出现该打印机则在“Administration”中添加打印机

![Printer](../img/services/cups/printer.avif)

7. 选择要共享的打印机，在下拉菜单中选择“Modify Printer”，然后勾选“Share this printer”

![Modify Printer](../img/services/cups/modify.avif)

![Share Printer](../img/services/cups/share.avif)

### 配置防火墙

```shell
sudo ufw allow ipp
sudo ufw allow mdns
```

## 客户端

### 打印机链接

将打印机管理页面地址中的`http`替换为`ipp`，删掉端口号，就是打印机的地址。

譬如管理地址是`https://172.16.77.66:631/printers/hp-LaserJet-1320-series`，
那么打印机地址就是`ipp://172.16.77.66/printers/hp-LaserJet-1320-series`。

![URL](../img/services/cups/url.avif)

### Windows

1. 打开设置->设备和打印机->添加打印机

2. 如果搜索不出来就选择“手动添加”

3. 选择IPP协议，填入打印机地址，然后点击“下一步”

### Kubunutu

1. 打开设置->打印机->添加打印机

2. 填入打印机地址，然后点击“下一步”

![Linux Client](../img/services/cups/linux.avif)
