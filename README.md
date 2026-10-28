# R50-WG50 一键安装

仅供测试。此安装会重写服务器系统盘并清除原系统，请先备份。适用于 x86_64 Linux 服务器；在 root 的 Bash 终端中粘贴下面整段命令。

```bash
curl -fL https://raw.githubusercontent.com/bin456789/reinstall/main/reinstall.sh -o reinstall.sh && bash reinstall.sh dd --img https://github.com/baby666666/test/releases/download/R50-WG50-test-20261028/iKuai8_x64_3.7.26_Enterprise_NativeRouting_R50_WG50_20261028_EFI_eth0-WAN-Web.img.gz
```

安装包：R50 50 接口测试镜像，监听 UDP 50001–50050。每次安装首次启动时生成一套服务端密钥和一套客户端密钥，由 50 组接口共用；各接口的隧道地址不同。
