
> 你打算买一台 VPS，但不知道延迟怎么样、线路稳不稳——所以你来搜"dmit looking glass"了。

这说明你挺谨慎的，买之前先测一测，这才是正确姿势。

DMIT 的 Looking Glass 工具就是为你这种人设计的：在掏钱之前，先用官方提供的测试节点 ping 一下、跑个 traceroute，看看数据包从你这边过去走的什么路、延迟多少毫秒。

这篇文章把 DMIT Looking Glass 的节点、用法、测试 IP 全部整理出来，顺带帮你搞清楚 DMIT 各条产品线到底有什么区别——毕竟它家的套餐名词有点多，第一次看确实容易懵。

---

## 什么是 Looking Glass，为什么值得用？

Looking Glass（简称 LG）是 ISP 或主机商公开的网络测试工具。它让你可以从**服务商的服务器端**主动发起网络测试，而不是从你自己的机器去 ping 服务器——方向反过来了，信息更完整。

通过 Looking Glass，你能看到：

- **Ping / RTT 延迟**：你的 IP 从 DMIT 节点过去要多少毫秒
- **Traceroute 路由路径**：数据包经过哪些节点、在哪里中转、有没有绕路
- **MTR 测试**：结合了 ping 和 traceroute，能看到每一跳的丢包率

这对判断一条线路是否"名副其实"非常重要。比如 DMIT 主打 CN2 GIA 和 CMIN2 优化线路，光看官网描述你不知道自己这边访问质量如何——但跑一下 Looking Glass 就清楚了。

---

## DMIT Looking Glass 入口

DMIT 官方 Looking Glass 地址：**[lg.dmit.sh](https://www.dmit.io/aff.php?aff=13832)**

> 👉 [点击访问 DMIT Looking Glass 测试工具](https://www.dmit.io/aff.php?aff=13832)

目前 DMIT Looking Glass 包含以下测试节点（根据搜索结果整理）：

| 节点名称 | 地区 | 线路类型 | 入口参数 |
|---|---|---|---|
| Los Angeles (Pro) | 美国洛杉矶 | CN2 GIA Premium | `?server=1` |
| Los Angeles (Eyeball) | 美国洛杉矶 | CMIN2 Eyeball | `?server=lax-eb` |
| Los Angeles (Tier 1) | 美国洛杉矶 | Tier 1 国际线路 | `?server=lax-t1` |
| Los Angeles (Premium Secure) | 美国洛杉矶 | CN2 GIA + 5Tbps DDoS 防护 | `?server=4` |
| Hong Kong (Pro) | 中国香港 | CN2 GIA + AS9929 + CMI | `?server=5` |
| Hong Kong (Eyeball) | 中国香港 | CMI Eyeball | `?server=6` |
| Hong Kong (Tier 1) | 中国香港 | 国际线路 | `?server=7` |
| Tokyo (Eyeball) | 日本东京 | 三网优化 | `?server=9` |

**各节点测试 IP 汇总：**

- 洛杉矶 Premium（LAX.Pro）测试 IPv4：`154.17.2.2`
- 洛杉矶 Eyeball（LAX.EB）测试 IPv4：`154.17.226.2`，IPv6：`2605:52c0:1:3:2c2a:59ff:fe05:65c2`
- 洛杉矶 Premium Secure（LAX.sPro）测试 IPv4：`45.88.194.2`
- 东京 Premium（TYO.Pro）测试 IPv4：`154.12.190.3`

---

## 如何使用 DMIT Looking Glass 测试网络质量

用法很简单，分三步：

**第一步：选择测试节点。** 打开 Looking Glass 页面后，从下拉菜单选择你想测的 DMIT 数据中心，比如你主要是想用洛杉矶线路，就选 LA Pro 或 LA Eyeball。

**第二步：输入你的 IP 地址或目标地址。** 直接输入你本机的公网 IP（可以先去 IP 查询网站查一下），然后选择 Ping、Traceroute 或 MTR 命令。

**第三步：分析结果。** 看延迟数值，一般电信/联通用户访问洛杉矶 CN2 GIA 线路，高峰期延迟能稳定在 150ms 左右算正常。如果 traceroute 显示路径经过 `59.43.x.x` 网段，说明走的是电信 CN2 GIA 骨干；看到 `AS58807` 则是 CMIN2。

---

## 四大使用场景：你适合哪条线路？

### 场景一：科学上网 / 代理服务

**推荐线路：LAX.Pro 或 LAX.EB**

对代理用途来说，最核心的诉求是稳定 + 低延迟 + 不被封。DMIT 洛杉矶 Premium 系列走三网 CN2 GIA 回程，高峰期延迟波动小；Eyeball 系列走 CMIN2，性价比更高。

两者都支持每 15 天免费换一次被墙 IP，这对代理用户是个很实际的保障。

通过 Looking Glass 测试时，选 LA Pro 节点，把你自己的 IP ping 一下，看延迟和丢包率。如果延迟在 150-180ms 且丢包接近 0%，基本可以放心买。

👉 [查看 DMIT 洛杉矶 Premium 套餐](https://www.dmit.io/aff.php?aff=13832&pid=100)

### 场景二：建站 / 面向国内用户的网站

**推荐线路：LAX.sPro 或 SJC.T1**

建站跟梯子不一样，你更在意的是抗 DDoS 和长期稳定，而不仅仅是延迟。

LAX.sPro 是 DMIT 洛杉矶高防系列，去程走 5Tbps+ 的 CFMT（Cloudflare Magic Transit）DDoS 防护线路，回程依然是 CN2 GIA。这意味着就算你被打，也有专业防御在扛着。

SJC.T1（圣何塞 Tier 1）自带 20Gbps DDoS 防御，走中国大陆常规优化线路，价格比洛杉矶 Pro 系列亲民不少，是建站性价比选择。

在 Looking Glass 里选 LA Premium Secure 节点测试 IP `45.88.194.2`，重点看高峰期（晚上 8-11 点）的稳定性。

👉 [查看 DMIT 洛杉矶高防套餐](https://www.dmit.io/aff.php?aff=13832&pid=130)

### 场景三：香港节点 / 低延迟优先

**推荐线路：HKG.Pro 或 HKG.EB**

如果你对延迟特别敏感——比如做游戏服务器或者需要实时通信——香港节点比洛杉矶物理距离近得多，理论上延迟会低 50-80ms。

HKG.Pro 是香港旗舰线路：电信走 CN2 GIA、联通走 AS9929、移动走 CMI，三网全优化。HKG.EB 则是 Eyeball 系列，价格更低，适合预算有限但想要香港节点的用户。

用 Looking Glass 的香港节点（`?server=5` 或 `?server=6`）从你的 IP 发起 ping，如果延迟能到 30-60ms 范围（国内用户），那体验相当不错。

👉 [查看 DMIT 香港 Premium 套餐](https://www.dmit.io/aff.php?aff=13832)

### 场景四：大流量 / 无限流量需求

**推荐线路：LAX.Pro.u 系列（Unmetered）或 SJC.T1**

如果你跑的业务流量消耗很大，按量计费的套餐会让你心跳加速，那就看 DMIT 的无限流量系列。

LAX.Pro.u 系列在 CN2 GIA 线路上提供不限制流量（但有带宽上限，从 30Mbps 到 200Mbps），适合需要长期稳定跑大量数据的场景。SJC.T1 也有 Unmetered 选项，年付可用优惠码 `SJC-Unmetered-Annually-30OFF` 打七折。

---

## DMIT 全套餐价格对比表

以下为 DMIT 当前主要套餐信息汇总，所有套餐均基于 KVM 虚拟化 + AMD EPYC 处理器 + SSD 存储，标配 1 IPv4 + 1 IPv6 /64（部分大型套餐含 2-3 个 IPv4）。

### 🇺🇸 洛杉矶 Premium（LAX.Pro）— CN2 GIA 三网优化

| 套餐名称 | 内存 | CPU | 硬盘 | 月流量 | 带宽 | 月付价格 | 购买 |
|---|---|---|---|---|---|---|---|
| LAX.Pro.WEE（年付特惠） | 1G | 1核 | 20G | 500G | 500Mbps | $36.9/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=183) |
| LAX.Pro.MALIBU（年付特惠） | 1G | 1核 | 20G | 1000G | 1Gbps | $49.9/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=186) |
| LAX.Pro.PalmSpring（年付特惠） | 2G | 2核 | 40G | 2000G | 2Gbps | $100/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=182) |
| LAX.Pro.TINY | 2G | 1核 | 20G | 1T | 1Gbps | $9.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=100) |
| LAX.Pro.Pocket | 2G | 1核 | 40G | 1.5T | 4Gbps | $14.90/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=137) |
| LAX.Pro.STARTER | 2G | 2核 | 80G | 3T | 10Gbps | $29.90/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=56) |
| LAX.Pro.MINI | 4G | 4核 | 80G | 5T | 10Gbps | $58.88/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=58) |
| LAX.Pro.MICRO | 4G | 4核 | 160G | 7T | 10Gbps | $74.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=81) |
| LAX.Pro.MEDIUM | 8G | 4核 | 160G | 14T | 10Gbps | $168.88/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=82) |
| LAX.Pro.LARGE | 16G | 8核 | 320G | 25T | 10Gbps | $338.88/月 |  [购买](https://www.dmit.io/aff.php?aff=13832) |
| LAX.Pro.GIANT | 24G | 12核 | 640G | 50T | 10Gbps | $619.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=98) |

### 🇺🇸 洛杉矶 Premium Unmetered（LAX.Pro.u）— CN2 GIA 不限流量

| 套餐名称 | 内存 | CPU | 硬盘 | 流量 | 带宽 | 价格 | 购买 |
|---|---|---|---|---|---|---|---|
| LAX.Pro.uMINI | 2G | 2核 | 20G | 不限 | 30Mbps | $239.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=62) |
| LAX.Pro.uMICRO | 8G | 4核 | 50G | 不限 | 50Mbps | $399.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=64) |
| LAX.Pro.uMEDIUM | 8G | 4核 | 80G | 不限 | 100Mbps | $799.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=65) |
| LAX.Pro.uLARGE | 16G | 8核 | 100G | 不限 | 200Mbps | $1399.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=66) |

### 🛡️ 洛杉矶 Premium Secure（LAX.sPro）— 5Tbps+ 高防 + CN2 GIA

| 套餐名称 | 内存 | CPU | 硬盘 | 月流量 | 带宽 | 价格 | 购买 |
|---|---|---|---|---|---|---|---|
| LAX.sPro.CREATOR | 2G | 2核 | 20G | 1.5T | 100Mbps | $71.99/季 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=130) |

### 🇺🇸 洛杉矶 Eyeball（LAX.EB）— CMIN2 三网优化

| 套餐名称 | 内存 | CPU | 硬盘 | 月流量 | 带宽 | 价格 | 购买 |
|---|---|---|---|---|---|---|---|
| LAX.EB.WEE（年付特惠） | 1G | 1核 | 20G | 1000G | 1Gbps | $39.9/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=188) |
| LAX.EB.CORONA（年付特惠） | 1G | 1核 | 20G | 1500G | 2Gbps | $49.9/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=218) |
| LAX.EB.FONTANA（年付特惠） | 2G | 2核 | 40G | 2500G | 4Gbps | $100/年 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=219) |
| LAX.EB.TINY | 2G | 1核 | 20G | 1.5T | 2Gbps | $9.99/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=189) |
| LAX.EB.Pocket | 2G | 1核 | 40G | 3T | 4Gbps | $14.90/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=190) |
| LAX.EB.STARTER | 2G | 2核 | 80G | 5T | 10Gbps | $29.90/月 |  [购买](https://www.dmit.io/aff.php?aff=13832&pid=191) |

### 🇭🇰 香港 Premium（HKG.Pro）— CN2 GIA + AS9929 + CMI

| 套餐名称 | 购买方式说明 | 购买 |
|---|---|---|
| HKG.Pro 系列（多配置可选） | 支持自定义升级 |  [查看所有香港套餐](https://www.dmit.io/aff.php?aff=13832) |

### 🇭🇰 香港 Tier 1（HKG.T1）— 国际线路（含大幅优惠）

| 套餐类型 | 优惠说明 | 优惠码 | 购买 |
|---|---|---|---|
| HKG.T1 年付 | 终身 45% 折扣 + 额外升配（更多 vCPU、双倍硬盘、50% 更多内存） | `HKG-T1-ANNUALLY-45OFF-RECUR` |  [购买](https://www.dmit.io/aff.php?aff=13832) |

### 🇯🇵 东京 Premium（TYO.Pro）— CN2 GIA + AS9929 + CMI

| 套餐类型 | 优惠说明 | 优惠码 | 购买 |
|---|---|---|---|
| TYO.Pro 月付 | 享受 10% 折扣 | `2025-TYO-T1-HI-GSL-MONTHLY-10OFF` |  [购买](https://www.dmit.io/aff.php?aff=13832) |
| TYO.Pro 季付 / 年付 | 终身 30% 折扣 | `2025-TYO-T1-HI-GSL-NON-MONTHLY-30OFF` |  [购买](https://www.dmit.io/aff.php?aff=13832) |

### 🇺🇸 圣何塞 Tier 1（SJC.T1）— 20Gbps DDoS 防御 + 国内优化

| 优惠说明 | 优惠码 | 购买 |
|---|---|---|
| 年付 Unmetered 套餐 30% 折扣 | `SJC-Unmetered-Annually-30OFF` |  [查看圣何塞套餐](https://www.dmit.io/aff.php?aff=13832) |

---

## 当前有效优惠码汇总（2026）

以下优惠码为社区整理，建议在结账时逐一尝试，DMIT 不定期调整有效期：

| 优惠码 | 适用范围 | 折扣力度 |
|---|---|---|
| `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF` | LAX.EB TINY 及以上，季付 / 年付 | 永久 8 折（循环） |
| `HKG-T1-ANNUALLY-45OFF-RECUR` | HKG.T1 年付 | 永久 55 折 + 升配 |
| `2025-TYO-T1-HI-GSL-NON-MONTHLY-30OFF` | TYO Tier 1 季付 / 年付 | 永久 7 折 |
| `2025-TYO-T1-HI-GSL-MONTHLY-10OFF` | TYO Tier 1 月付 | 月付 9 折 |
| `SJC-Unmetered-Annually-30OFF` | SJC 不限流量年付 | 年付 7 折 |
| `2025-XMAS-LAX-T1-10-OFF-RECURRING` | LAX Tier 1 | 循环 9 折 |
| `202510_HKG_TYO_PRO_20OFF_RECURRING` | HKG / TYO Pro 季付及以上 | 循环 8 折 |
| `7L8O3PQTHNXCFS2TXPLP` | 多数套餐非月付适用 | 额外 95 折 |

---

## 几个值得知道的细节

**IP 被墙怎么办？** DMIT 提供免费换 IP 政策：购买满 7 天后，每 15 天可免费申请更换一次被封锁的 IP。这对代理用途来说非常实用，其他情况下换 IP 收费 $5/次。

**硬件是什么级别的？** DMIT 全线使用 AMD EPYC 处理器（洛杉矶节点以 9004/9005 系列为主，香港和东京以 7003 系列为主），搭配企业级 SSD，磁盘 I/O 实测普遍超过 839MB/s。比那些还在用 Intel Xeon E5 的厂商确实强一个量级。

**流量超了怎样？** DMIT 不会直接断网，而是把带宽限速到 100Mbps-1Gbps 之间继续使用，下个月重置后自动恢复正常速度。

**支付方式？** 支持 PayPal、支付宝、微信支付、信用卡（Visa/MasterCard）、加密货币（Bitcoin 等），支付场景很全面。

---

## 总结：先测再买，心里有底

DMIT Looking Glass 是这家服务商做得比较到位的一个细节——直接开放各地节点给你测，不怕比较，因为线路质量确实在那里。

用法很简单：先去 Looking Glass 页面选你打算买的节点，把自己的 IP 跑一遍 traceroute，看路由经过哪里、延迟多少。国内用户测洛杉矶 CN2 GIA，高峰期延迟能稳在 150ms 左右就算优秀；香港节点如果能 30-60ms 那就相当不错了。

测完满意了，再结合上面的套餐表和优惠码，选一个最适合自己场景的方案。

👉 [前往 DMIT 官网查看当前可用套餐](https://www.dmit.io/aff.php?aff=13832)
