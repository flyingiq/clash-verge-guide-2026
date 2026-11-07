> 📅 最后更新：2026-11-07 · 节点与套餐信息实时同步

# 🧩 Clash Verge Rev 完整使用指南（2026）

> 从安装到 TUN 模式、规则分流、订阅管理的全流程实操文档。
> 适合 Windows / macOS / Linux 桌面端用户。

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-blue)]()
[![Updated](https://img.shields.io/badge/Updated-2026--11-brightgreen)]()
[![Guide](https://img.shields.io/badge/Type-Tutorial-orange)]()

📖 配套机场推荐与节点测速：[2026 最新平价稳定机场推荐](https://github.com/flyingiq/airport-recommended-2026)

---

## 目录

- [一、Clash Verge Rev 是什么](#一clash-verge-rev-是什么)
- [二、安装](#二安装)
- [三、导入订阅](#三导入订阅)
- [四、TUN 模式（全局接管）](#四tun-模式全局接管)
- [五、规则与分流策略](#五规则与分流策略)
- [六、常见问题排查](#六常见问题排查)

---

## 一、Clash Verge Rev 是什么

Clash Verge Rev 是 Clash Verge 的活跃维护分支，内核为 **Mihomo（Clash.Meta）**。
相比原版 Clash for Windows，它支持：

- VLESS / REALITY / Hysteria2 / TUIC 等新协议
- TUN 模式（无需设置系统代理，全局接管流量）
- 多订阅管理与自动更新
- 规则集可视化编辑
- 内置测速与延迟排序

**适用场景**：桌面端日常使用、开发调试、需要分流的办公环境。

---

## 二、安装

### Windows

1. 下载 `Clash.Verge_x.x.x_x64-setup.exe`
2. 安装时建议勾选「为所有用户安装」
3. 首次启动会提示安装服务（TUN 模式依赖），点「是」

### macOS

```bash
brew install --cask clash-verge-rev
```

或下载 `.dmg` 拖入 Applications。
首次运行需在「系统设置 → 隐私与安全性」允许系统扩展。

### Linux

```bash
# Debian / Ubuntu
wget -O clash-verge.deb https://github.com/clash-verge-rev/clash-verge-rev/releases/latest/download/clash-verge_x64.deb
sudo dpkg -i clash-verge.deb
```

---

## 三、导入订阅

1. 打开 Clash Verge Rev → **订阅** → **新建**
2. 填入订阅链接，类型选 **Remote**
3. 点击「更新」，等待节点列表出现
4. 在「代理」页选择节点或策略组

**订阅格式说明**：

| 客户端 | 订阅后缀 | 说明 |
|---|---|---|
| Clash Verge Rev | `/clash_meta` 或直接原链接 | 推荐 meta 格式 |
| ClashX | `/clash` | 旧版兼容 |
| sing-box | `/sing_box` | 独立格式 |

多数机场会按 User-Agent 自动返回对应格式，直接粘贴原链接即可。

---

## 四、TUN 模式（全局接管）

**TUN 模式让所有程序（包括不认系统代理的）都走代理。**

步骤：

1. 设置 → **TUN 模式** → 开启
2. Windows 会安装 `wintun` 驱动，允许即可
3. macOS 需授权系统扩展
4. 开启后「系统代理」可以关掉（TUN 已接管）

**注意事项**：

- 开了 TUN 后，Docker / WSL / 虚拟机流量也会被接管
- 公司内网 VPN 可能与 TUN 冲突，需要配置 `route-exclude-address`
- 如果开 TUN 后断网，先进「设置 → 关闭 TUN」恢复

---

## 五、规则与分流策略

**推荐的分流结构**：

```yaml
rules:
  - DOMAIN-SUFFIX,cn,DIRECT
  - GEOIP,CN,DIRECT
  - DOMAIN-SUFFIX,openai.com,AI
  - DOMAIN-SUFFIX,github.com,PROXY
  - MATCH,PROXY
```

**策略组建议**：

```
🚀 节点选择     → 手动选 / 自动测速
♻️ 自动选择     → url-test，300 秒测一次
🌍 国外媒体     → 流媒体专用节点
🎯 全球直连     → DIRECT
🛑 广告拦截     → REJECT
```

**关键原则**：

- 国内域名走 DIRECT，避免绕路
- 流媒体单独分组（原生 IP 节点成功率更高）
- AI 类服务单独分组（部分地区被限制）

---

## 六、常见问题排查

| 现象 | 原因 | 处理 |
|---|---|---|
| 订阅更新失败 | 链接被墙 / UA 不匹配 | 换备用订阅地址，或开代理后更新 |
| 开 TUN 后断网 | 路由冲突 | 关闭 TUN，检查 `route-exclude-address` |
| 部分网站打不开 | 规则误判 | 把域名加进 `DIRECT` 或 `PROXY` 规则 |
| 速度很慢 | 节点拥塞 | 用 url-test 自动选优，或手动换节点 |
| Clash 启动闪退 | 配置语法错误 | 查看日志页的报错行号 |

---

## 七、稳定节点从哪来

自建或选购时重点关注：

- **协议**：优先 VLESS + REALITY，抗封锁能力最强
- **IP 类型**：原生 IP 对流媒体和 AI 服务更友好
- **线路**：CN2 GIA / 软银 / 9929 等优化线路延迟更低
- **节点数量**：多地区冗余，单一节点故障不影响使用

📌 我自己在用的方案与实测数据整理在这里：
**[2026 最新平价稳定机场推荐（含节点测速与避坑）](https://github.com/flyingiq/airport-recommended-2026)**

🌐 商城：https://two.harnesscom.com
📊 节点状态：https://status.harnesscom.com

---

## 许可

文档内容 MIT。工具版权归各自项目所有。
