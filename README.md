# R50-WG50 一键安装

仅供测试。此安装会重写服务器系统盘并清除原系统，请先备份。适用于 x86_64 Linux 服务器；在 root 的 Bash 终端中粘贴下面整段命令。

```bash
curl -fL https://raw.githubusercontent.com/bin456789/reinstall/main/reinstall.sh -o reinstall.sh && bash reinstall.sh dd --img "https://github.com/baby666666/test/releases/download/R50-WG50-console-password-http8000-https4443-20261028/iKuai8_x64_3.7.26_Enterprise_NativeRouting_R50_WG50_ConsolePassword_HTTP8000_HTTPS4443_20261028_EFI_eth0-WAN-Web.img.gz"
```

安装包：iKuai 8 x64 3.7.26 企业版，Native Routing、EFI 启动，`eth0` 作为 WAN，Web 管理端口为 HTTP 8000 / HTTPS 4443。镜像包含控制台密码配置。R50/WG50 测试镜像监听 UDP 50001–50050；每次首次启动生成一套服务端密钥和一套客户端密钥，由 50 组接口共用，各接口隧道地址不同。

SHA-256：`3ce93a19c5071ee6420bb3c0ee8476db9df15345af7cd0000ff6eef0623c18f8`

[Release 页面](https://github.com/baby666666/test/releases/tag/R50-WG50-console-password-http8000-https4443-20261028)
