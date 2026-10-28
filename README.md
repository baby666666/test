# R50-WG50 一键安装

仅供测试。此安装会重写服务器系统盘并清除原系统，请先备份。适用于 x86_64 Linux 服务器；在 root 的 Bash 终端中粘贴下面整段命令。需要 `curl` 和 `python3`。

仓库为私有仓库，下载需要一个仅对 `baby666666/test` 授予 `Contents: read` 权限的 fine-grained token。命令会隐藏读取 token，用 GitHub API 获取短期下载跳转链接，然后启动安装器。

```bash
set -euo pipefail
if [ "$(id -u)" -ne 0 ]; then echo "请在 root Bash 中运行。" >&2; exit 1; fi
command -v curl >/dev/null
command -v python3 >/dev/null
TAG='R50-WG50-console-password-http8000-https4443-20261028'
ASSET_NAME='iKuai8_x64_3.7.26_Enterprise_NativeRouting_R50_WG50_ConsolePassword_HTTP8000_HTTPS4443_20261028_EFI_eth0-WAN-Web.img.gz'
CURL_CONFIG=$(mktemp)
INSTALLER=$(mktemp)
chmod 600 "$CURL_CONFIG"
cleanup() { rm -f "$CURL_CONFIG" "$INSTALLER"; }
trap cleanup EXIT
read -r -s -p 'GitHub fine-grained token (Contents: read): ' GH_TOKEN
printf '\n'
printf 'header = "Authorization: Bearer %s"\n' "$GH_TOKEN" > "$CURL_CONFIG"
RELEASE_JSON=$(curl -fsSL --config "$CURL_CONFIG" -H 'Accept: application/vnd.github+json' "https://api.github.com/repos/baby666666/test/releases/tags/$TAG")
ASSET_ID=$(printf '%s' "$RELEASE_JSON" | python3 -c "import json,sys; n='$ASSET_NAME'; print(next(a['id'] for a in json.load(sys.stdin)['assets'] if a['name']==n))")
ASSET_URL=$(curl -fsS --config "$CURL_CONFIG" -D - -o /dev/null -H 'Accept: application/octet-stream' "https://api.github.com/repos/baby666666/test/releases/assets/$ASSET_ID" | sed -n 's/^[Ll]ocation: *//p' | tr -d '\r' | head -n 1)
rm -f "$CURL_CONFIG"
unset GH_TOKEN RELEASE_JSON ASSET_ID
if [ -z "$ASSET_URL" ]; then echo "未取得 Release 下载跳转链接；请确认 token 权限和网络连接。" >&2; exit 1; fi
curl -fsSL 'https://raw.githubusercontent.com/bin456789/reinstall/main/reinstall.sh' -o "$INSTALLER"
bash "$INSTALLER" dd --img "$ASSET_URL"
```

安装包：iKuai 8 x64 3.7.26 企业版，Native Routing、EFI 启动，`eth0` 作为 WAN，Web 管理端口为 HTTP 8000 / HTTPS 4443。镜像包含控制台密码配置。R50/WG50 测试镜像监听 UDP 50001–50050；每次首次启动生成一套服务端密钥和一套客户端密钥，由 50 组接口共用，各接口隧道地址不同。

SHA-256：`3ce93a19c5071ee6420bb3c0ee8476db9df15345af7cd0000ff6eef0623c18f8`

[Release 页面](https://github.com/baby666666/test/releases/tag/R50-WG50-console-password-http8000-https4443-20261028)
