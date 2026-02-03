# Trojan 代理工具安装指南及替代方案

> 本指南介绍 Trojan 翻墙工具的安装使用方法，以及 2025-2026 年更先进的替代方案。

## 目录

- [Trojan 简介](#trojan-简介)
- [Trojan 安装方法](#trojan-安装方法)
- [客户端配置](#客户端配置)
- [更好的替代方案](#更好的替代方案)
- [方案对比与推荐](#方案对比与推荐)

---

## Trojan 简介

Trojan 是一个开源的代理工具，其核心思想是将流量伪装成正常的 **HTTPS 通信**。它通过监听 443 端口，模仿互联网上最常见的 HTTPS 协议，完成真正的 TLS 握手，从而诱骗防火墙认为它就是普通的 HTTPS 流量。

### 特点

- 轻量级，专注于绑过防火墙
- 配置相对简单，适合新手
- 伪装性好，流量看起来像访问正常网站
- 相比 V2Ray 功能较少，但更简洁

---

## Trojan 安装方法

### 方法一：一键安装脚本（推荐新手）

**前提条件：**
- 一台境外 VPS 服务器（推荐 Debian/Ubuntu 系统）
- 一个域名（可使用免费域名）
- 域名已解析到 VPS IP

**安装步骤：**

```bash
# 1. 更新系统
apt update && apt upgrade -y

# 2. 安装必要工具
apt install -y curl wget

# 3. 运行一键安装脚本（以 Jrohy 脚本为例）
source <(curl -sL https://git.io/trojan-install)
```

脚本会自动：
- 安装 Trojan 最新版本
- 申请 SSL 证书（Let's Encrypt）
- 配置 Nginx 伪装网站
- 生成客户端配置

### 方法二：手动安装

```bash
# 1. 安装依赖
apt install -y nginx certbot python3-certbot-nginx

# 2. 申请 SSL 证书
certbot --nginx -d your-domain.com

# 3. 下载 Trojan
wget https://github.com/trojan-gfw/trojan/releases/download/v1.16.0/trojan-1.16.0-linux-amd64.tar.xz
tar -xf trojan-1.16.0-linux-amd64.tar.xz
cd trojan

# 4. 编辑配置文件
nano config.json
```

**服务端配置示例 (config.json)：**

```json
{
    "run_type": "server",
    "local_addr": "0.0.0.0",
    "local_port": 443,
    "remote_addr": "127.0.0.1",
    "remote_port": 80,
    "password": ["your-password-here"],
    "ssl": {
        "cert": "/etc/letsencrypt/live/your-domain.com/fullchain.pem",
        "key": "/etc/letsencrypt/live/your-domain.com/privkey.pem"
    }
}
```

```bash
# 5. 启动 Trojan
./trojan -c config.json
```

### 方法三：Trojan-Go（支持 CDN）

Trojan-Go 是 Trojan 的增强版，支持 WebSocket + CDN，可以保护 VPS IP 不被封锁。

```bash
# 安装 Trojan-Go
bash <(curl -sL https://raw.githubusercontent.com/p4gefau1t/trojan-go/master/install_script/install.sh)
```

---

## 客户端配置

### Windows
- **v2rayN** - 支持多协议，推荐
- **Clash Verge** - 界面美观
- **NekoRay** - 功能强大

### macOS
- **ClashX Pro** - 推荐
- **V2rayU**
- **Stash**

### iOS
- **Shadowrocket** (小火箭) - 付费，最推荐
- **Stash** - 付费
- **Quantumult X** - 付费

### Android
- **v2rayNG** - 免费，推荐
- **Clash for Android**
- **NekoBox for Android**
- **sing-box** - 免费

### Linux
```bash
# 使用命令行客户端
./trojan -c client-config.json
```

---

## 更好的替代方案

随着技术发展，目前有几种比 Trojan 更先进的方案：

### 1. VLESS + Reality (Xray) ⭐⭐⭐⭐⭐

**目前抗封锁能力最强的方案**

Reality 通过"借用"真实网站的 TLS 指纹来伪装，无需自己的域名和证书，能有效抵抗基于 TLS 特征的检测。

**优点：**
- 无需域名和证书
- 伪装性极强，流量特征与真实 HTTPS 一致
- 能穿透审查最严的地区（如伊朗、某些省份）

**安装：**

```bash
# Xray 一键安装脚本
bash <(curl -sL https://raw.githubusercontent.com/XTLS/Xray-install/main/install-release.sh)
```

**配置示例：**

```json
{
    "inbounds": [{
        "port": 443,
        "protocol": "vless",
        "settings": {
            "clients": [{"id": "uuid-here", "flow": "xtls-rprx-vision"}],
            "decryption": "none"
        },
        "streamSettings": {
            "network": "tcp",
            "security": "reality",
            "realitySettings": {
                "dest": "www.microsoft.com:443",
                "serverNames": ["www.microsoft.com"],
                "privateKey": "your-private-key",
                "shortIds": [""]
            }
        }
    }]
}
```

### 2. Hysteria2 ⭐⭐⭐⭐

**适合网络质量差的环境**

基于 QUIC (HTTP/3) 协议，专为不稳定网络优化。在高丢包率环境下性能提升可达 50 倍。

**优点：**
- 高丢包网络下表现优异
- 速度快，延迟低
- 支持大流量场景

**缺点：**
- 需要开放 UDP 端口
- GFW 可能针对长时间 UDP 通信

**安装：**

```bash
# Hysteria2 一键安装
bash <(curl -fsSL https://get.hy2.sh/)
```

### 3. Sing-box ⭐⭐⭐⭐

**新一代代理平台的"瑞士军刀"**

Sing-box 支持多种协议，全平台 GUI 客户端，iOS 端还是免费的。

**优点：**
- 支持协议丰富（SS、VMess、VLESS、Hysteria2、WireGuard 等）
- 全平台支持，iOS 免费
- 性能优秀，资源占用低
- 可作为客户端使用多种协议

**安装：**

```bash
# 安装 sing-box
bash <(curl -fsSL https://sing-box.app/deb-install.sh)
```

---

## 方案对比与推荐

| 特性 | Trojan | VLESS+Reality | Hysteria2 | Sing-box |
|------|--------|---------------|-----------|----------|
| 抗封锁能力 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | 取决于协议 |
| 配置难度 | 简单 | 中等 | 简单 | 中等 |
| 速度 | 良好 | 良好 | 极佳(差网络) | 良好 |
| 需要域名 | 是 | 否 | 是 | 取决于协议 |
| 协议类型 | TCP/TLS | TCP/Reality | UDP/QUIC | 多协议支持 |

### 2025-2026 推荐方案

1. **首选：VLESS + Reality**
   - 抗检测能力最强
   - 无需域名证书
   - 适合长期稳定使用

2. **网络质量差：Hysteria2**
   - 高丢包环境性能优异
   - 适合移动网络

3. **新手入门：Trojan**
   - 配置简单
   - 教程丰富
   - 适合学习理解代理原理

4. **多协议需求：Sing-box**
   - 一个客户端支持所有协议
   - 灵活切换

---

## 注意事项

1. **合规使用**：请遵守当地法律法规，合理使用代理工具
2. **安全第一**：定期更新软件，使用强密码
3. **备份配置**：保存好服务器和客户端配置
4. **多节点备份**：建议准备多个节点以防单点故障

---

## 参考资料

- [Trojan 官方 GitHub](https://github.com/trojan-gfw/trojan)
- [Xray-core 官方文档](https://xtls.github.io/)
- [Hysteria 官方网站](https://hysteria.network/)
- [Sing-box 官方文档](https://sing-box.sagernet.org/)

---

*最后更新：2026年2月*
