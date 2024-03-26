# Docker-SMTP
[![](https://images.microbadger.com/badges/image/namshi/smtp.svg)](https://microbadger.com/images/namshi/smtp)

这是一个用于发送电子邮件的 SMTP docker 容器。您还可以将电子邮件中继到 gmail 和 amazon SES。

## 环境变量

容器接受必须以“：”开头的“RELAY_NETWORKS”环境变量，例如“：192.168.0.024”或“：192.168.0.024：10.0.0.016”。

容器接受“KEY_PATH”和“CERTIFICATE_PATH”环境变量，如果提供这些变量，则将启用 TLS 支持。这些路径必须指向公开卷上的密钥和证书文件。密钥将复制到容器位置。

容器接受“MAILNAME”环境变量，该变量将设置传出邮件主机名。

容器还接受“PORT”环境变量，以设置邮件守护程序将在容器内侦听的端口。默认端口为“25”。

要配置绑定地址，您可以使用“BIND_IP”和“BIND_IP6”环境变量。默认的“BIND_IP”为“0.0.0.0”。默认的“BIND_IP6”为“：：0”。

要禁用 IPV6，您可以将“DISABLE_IPV6”环境变量设置为任何值。

容器接受“OTHER_HOSTNAMES”环境变量，该变量将设置此计算机应将自己视为最终目标的域列表。

## 下面是使用此容器的方案

### 作为 SMTP 服务器
您无需指定任何环境变量即可实现此功能。

### 作为辅助 SMTP 服务器
指定“RELAY_DOMAINS”以设置应接受哪些域以转发到距离较短的 MX 服务器。

格式为 '<domain1> ： <domain2> ： <domain3> etc'

### 作为 Gmail 中继
您需要设置“GMAIL_USER”和“GMAIL_PASSWORD”才能使用它。

### 作为通用 SMTP 中继
您还可以使用任何具有身份验证作为智能主机的通用 SMTP 服务器。</br>
您需要设置 'SMARTHOST_ADDRESS'、'SMARTHOST_PORT'（连接参数）、'SMARTHOST_USER'、'SMARTHOST_PASSWORD'（身份验证参数）和 'SMARTHOST_ALIASES'：这是用于身份验证的 puth 身份验证数据的别名列表，分号分隔。<br>

```
Example:

 * SMARTHOST_ADDRESS=mail.mysmtp.com
 * SMARTHOST_PORT=587
 * SMARTHOST_USER=myuser
 * SMARTHOST_PASSWORD=secret
 * SMARTHOST_ALIASES=*.mysmtp.com
```
