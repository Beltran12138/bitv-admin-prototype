# BitV Admin 后台系统原型

**在线预览** → [https://beltran12138.github.io/bitv-admin-prototype/](https://beltran12138.github.io/bitv-admin-prototype/)

---

## 项目背景

**BitV（BitValve）** 是一家在香港证监会（SFC）监管下运营的虚拟资产交易平台（VATP），提供 USDT 计价的永续合约交易服务。

本原型基于以下文件深度梳理后设计：
- SFC ASPIRe 路线图 PillarP（2026-02-11 发布）
- 币安合约功能模块深度分析
- CEX 永续合约设计路线图
- 香港离岸所合约交易差异对比

**核心合规约束：**
- 仅对**专业投资者（PI）**开放（个人：投资组合 ≥ HKD 800 万；机构：≥ HKD 4000 万）
- 最高杠杆 **20x**（vs. 离岸所 125x）
- 保证金抵押品仅限 HKMA 监管稳定币（USDT/USDC）
- 保险基金须**实时公开披露**（SFC 强制要求）
- ADL 触发后 **24 小时内**出具书面事后报告

---

## 页面清单

| 页面 | 模块名称 | 核心功能 |
|------|---------|---------|
| [01\_总控台.html](01_总控台.html) | **总控台** | 全平台实时 KPI、保证金率分布、高危账户预警、ADL Top-5、系统状态、资金费率倒计时 |
| [02\_用户管理.html](02_用户管理.html) | **用户管理 / PI 审核** | PI 资质审批队列、KYC-3 状态追踪、用户账户管理、SFC 合规档案 |
| [03\_风控监控.html](03_风控监控.html) | **风控监控** | 24H 保证金率趋势（max/avg/P90）、指数价格源偏差监控、高危仓位明细、风险日志 |
| [04\_强平管理.html](04_强平管理.html) | **强制平仓管理** | SFC 第19条五层强平瀑布流程图、7日强平量图表、强平历史记录 |
| [05\_保险基金.html](05_保险基金.html) | **保险基金** | SFC 强制实时披露、三池分布、30日趋势图、合规清单、压力测试结果 |
| [06\_ADL系统.html](06_ADL系统.html) | **ADL 自动减仓** | 排名公式（PNL% × 有效杠杆）、5灯指示器、24H 事后报告归档管理 |
| [07\_合约配置.html](07_合约配置.html) | **合约配置** | 合约列表、阶梯保证金7档、交易参数、风控参数、双人授权变更、审计日志 |
| [08\_资金费率.html](08_资金费率.html) | **资金费率监控** | 实时倒计时、费率分量拆解（TWAP + 固定利率公式）、30日历史、跨所对比 |

---

## 设计规范

### 色彩系统

| Token | 色值 | 用途 |
|-------|------|------|
| `--bg` | `#060C18` | 页面底色 |
| `--surface` | `#0B1220` | 侧边栏/顶栏 |
| `--card` | `#0F1A2E` | 卡片背景 |
| `--cyan` | `#00C6E0` | 主强调色 / 交互元素 |
| `--indigo` | `#7C78EE` | 次要强调色 |
| `--success` | `#00D4A0` | 正常 / 盈利 |
| `--warning` | `#FFB300` | 预警 |
| `--danger` | `#FF4757` | 危险 / 亏损 |

### 字体

| 用途 | 字体 |
|------|------|
| 标题 / Display | Syne 700/800 |
| 正文 | Plus Jakarta Sans 400/500/600 |
| 数字 / 代码 | Space Mono 400 |
| 中文回退 | PingFang SC → Microsoft YaHei |

### 依赖

- **Chart.js 4.4** — 折线图、柱状图（CDN 加载）
- **Google Fonts** — 字体（CDN 加载）
- 无其他框架依赖，纯 HTML + CSS + Vanilla JS

---

## 本地查看

直接用浏览器打开 `index.html`，或任意 HTML 文件：

```bash
# macOS / Linux
open index.html

# Windows（任选其一）
start index.html
# 或在文件管理器中双击 index.html
```

> 需要联网加载 Google Fonts 和 Chart.js；断网情况下字体回退至系统中文字体，图表不可用。

---

## 强平层级（SFC 第19条）

```
1. 订单簿止损（Order Book Liquidation）  ← 优先尝试
2. 备用流动性提供方（Backstop Liquidity Provider）
3. 保险基金（Insurance Fund）            ← SFC 强制实时披露
4. ADL 自动减仓（Auto-Deleveraging）     ← SFC 强制24H事后报告
5. 最终兜底机制（Last Resort）
```

---

*本原型仅供内部评审使用，不构成正式产品交付物。*
