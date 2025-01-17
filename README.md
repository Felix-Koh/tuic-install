## [TUIC](https://github.com/EAimTY/tuic)安装指南(Quick Installation Guide)
## forked from [chika0801/tuic-install](https://github.com/chika0801/tuic-install)

1. 下载程序(Download TUIC)

linux-amd64
```
curl -Lo /root/tuic https://github.com/EAimTY/tuic/releases/download/0.8.4/tuic-server-0.8.4-x86_64-linux-musl && chmod +x /root/tuic
```

2. 下载配置(Download config)

```
curl -Lo /root/tuic_config.json https://raw.githubusercontent.com/Felix-Koh/tuic-install/main/config_server.json
```

3. 下载systemctl配置(Download systemctl config)

```
curl -Lo /etc/systemd/system/tuic.service https://raw.githubusercontent.com/chika0801/tuic-install/main/tuic.service
```

4. 上传证书和私钥(Upload certificate and private key)

- 将证书文件改名为`fullchain.cer`，将私钥文件改名为`private.key`，使用WinSCP登录你的VPS，将它们上传到`/root/`目录。(Rename the certificate file to `fullchain.cer` and the private key file to `private.key`, log in to your VPS using WinSCP, upload them to the `/root/` directory.)
- [用acme申请 SSL 证书](https://github.com/chika0801/Xray-install#1%E7%94%A8acme%E7%94%B3%E8%AF%B7-ssl-%E8%AF%81%E4%B9%A6)

5. 启动程序(Start TUIC)

```
systemctl daemon-reload && systemctl enable --now tuic
```

```
systemctl status tuic
```

| 项目 | |
| :--- | :--- |
| 程序(TUIC file) | /root/tuic |
| 配置(config) | /root/tuic_config.json |
| 证书(certificate) | /root/fullchain.cer |
| 私钥(private key) | /root/private.key |
| systemctl配置(systemctl config) | /etc/systemd/system/tuic.service |
| 查看日志(view log) | journalctl -u tuic --output cat -e |
| 实时日志(real-time logs) | journalctl -u tuic --output cat -f |

## v2rayN配置指南

1. 下载Windows客户端程序[tuic-client-0.8.4-x86_64-windows-msvc.exe](https://github.com/EAimTY/tuic/releases/download/0.8.4/tuic-client-0.8.4-x86_64-windows-msvc.exe)，重命令为`tuic.exe`，复制到v2rayN文件夹。

2. 下载客户端配置[config_client.json](https://github.com/chika0801/tuic-install/blob/main/config_client.json)，修改`chika.example.com`为证书中包含的域名，修改`10.0.0.1`为VPS的IP。

3. `服务器` ——> `添加自定义配置服务器` ——> `浏览(B)` ——> `选择客户端配置` ——> `Core类型 tuic` ——> `Socks端口 50001`

![1](https://user-images.githubusercontent.com/88967758/195763590-f035f90f-f228-4022-b318-770791c63b92.jpg)

小技巧：只要证书在有效期内，证书中包含的域名不用解析到VPS的IP。一份证书，在多个VPS上使用。
