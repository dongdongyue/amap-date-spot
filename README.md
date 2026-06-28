<div align="center">

# 💕 Date Spot — 智能约会助手

**找个地方 + 规划动线 + 生成邀请卡片。一句话 → 一张可以发给 ta 的约会请帖。**

*Venue discovery + itinerary planning + shareable invitation card. One sentence → one date.*

[![Amap Skill](https://img.shields.io/badge/高德地图-Skill-blue)](https://lbs.amap.com/)
[![Version](https://img.shields.io/badge/version-1.0.0-green)]()
[![Platform](https://img.shields.io/badge/platform-Claude%20Code%20%7C%20OpenClaw-blueviolet)]()

[快速开始](#安装) · [示例](#示例) · [核心功能](#核心功能) · [安装](#安装) · [使用](#使用) · [常见问题](#常见问题)

> 🆕 **约会邀请卡片**：生成一个 HTML 文件，发给她/他——地图、动线、时间、着装建议，一张卡片搞定。约人不用打 10 行字。

[中文](#-场景) | [English](#-scenario)

</div>

---

## 📖 场景

> 小林，大四，终于鼓起勇气约了隔壁班的女生见面。
>
> 她在河西万达，他在大行宫，两人约好找个中间的地方。**但去哪呢？**
>
> 打开大众点评满屏推荐，不知道哪家安静适合聊天；百度搜"南京约会地点"，全是营销号软文。
>
> 他在 AI 助手里说了一句：**"我在大行宫，她在河西万达，找个中间的地方，第一次见面"**

然后，Date Spot 帮他找到了一家步行 4 分钟的湖边咖啡馆，附上了导航链接。

```
📍 推荐区域：莫愁湖附近

1. ☕ 湖畔咖啡馆 — 浪漫
   📌 莫愁路 88 号 · 步行约 4 分钟
   🟢 营业中
   🚶 你 地铁15分钟 | 她 步行8分钟
   ✨ 靠窗位能看到湖景，安静适合聊天

2. 🌿 莫愁湖公园 — 轻松
   📌 水西门大街 · 步行约 6 分钟
   🟢 营业中
   🚶 你 地铁18分钟 | 她 步行10分钟
   ✨ 今天天气好，湖边散步很舒服

3. 📚 先锋书店 — 文艺
   📌 五台山体育馆 · 步行约 12 分钟
   🟢 营业中
   🚶 你 地铁22分钟 | 她 步行15分钟
   ✨ 南京地标级书店，有咖啡区可以坐下来聊

🏆 如果只选一个：选湖畔咖啡馆——离双方都近，安静，靠窗有湖景
```

---

## ✨ 核心功能

| 你只需要说 | 助手帮你做 |
|:---|:---|
| "第一次见面，在 XX" | 12 种时段模式匹配 → 周边搜索 → 筛选排除 → 3 个推荐 + 动线 |
| "我在 XX，她在 YY" | 地理编码 → 计算中点 → 分别算通勤时间 → 公平性评估 |
| "生成邀请卡片" | 🆕 生成约会邀请卡 HTML——发给 ta，地图/动线/着装一页搞定 |
| "都不喜欢，太贵了" | 解析不满原因 → 缩小范围 → 推荐 3 个新的 |
| 未指定时间/菜系/性别 | 逐项追问确认，不猜不假设 |

### 🎯 智能风格推断

根据你说话的方式自动匹配推荐风格：

| 你说的 | 助手理解的 | 偏向搜索 |
|:---|:---|:---|
| "第一次见面""约会""表白" | 🌹 浪漫 | 咖啡馆 + 公园 + 甜品 |
| "朋友聚聚""喝一杯""随意" | 🍻 轻松 | 小酒馆 + 轻食 + 公园 |
| "看书""安静""文艺" | 📖 文艺 | 书店 + 咖啡馆 + 美术馆 |
| "谈事""客户""正式" | 💼 商务 | 茶馆 + 咖啡厅 + 安静餐厅 |

### 🚶 双方通勤时间

不只是推荐"好地方"——推荐"对你们俩都方便的好地方"。

```
🚶 你 地铁15分钟 | 她 步行8分钟     ← 公平！
🚶 你 地铁35分钟 | 她 步行5分钟     ← 不太公平，会注明
```

### 🌦️ 天气联动

搜索前自动查天气，下雨天不会推荐你去公园淋雨：

- 晴天 → 公园优先，"傍晚去光线好"
- 下雨 → 只推室内，"今天有阵雨，推荐的都是室内好去处"
- 高温/严寒 → 优先有空调/暖气的地方

### 💬 一键约人消息

选好地方后说"帮我写个约她的消息"，生成自然口语的邀请文字：

```
我在莫愁湖附近找到了一个挺安静的咖啡馆，靠窗能看到湖景。
你从河西万达过来只要步行 8 分钟，现在正好营业中。
地址是莫愁路 88 号，到了我发你定位 👉 https://uri.amap.com/marker?...
```

直接复制发给对方，不像营销文案。

### 💌 约会邀请卡片（HTML）

说"生成邀请卡片"或"帮我做个邀请"，生成一张可**直接发给对方**的约会请帖 HTML：
- 🗺️ 上半屏：高德交互地图，会面点+推荐点+路线一目了然
- 💌 下半屏：动线时间轴 + 地点卡片 + 着装建议 + 礼物提示
- 🎨 粉色渐变设计，像请帖不像工具页
- 📱 移动端优先，微信直接打开
- 🔗 底部一键导航按钮，点击跳转高德地图

> **约人不用打 10 行字**。选好地方 → 生成邀请卡 → 发 HTML 给她/他。一页包含所有信息。

---

## 🎯 适合谁

| 场景 | 痛点 | Date Spot 怎么帮 |
|:---|:---|:---|
| 相亲/第一次见面 | 不知道去哪，怕太尴尬 | 推荐安静适合聊天的地方，附氛围描述 |
| 朋友约见面 | 两人位置不同，找中间点麻烦 | 自动算中点 + 分别算通勤时间 |
| 商务约见 | 需要得体但不太正式 | 商务风格推断：茶馆、安静咖啡厅 |
| 老夫老妻约会 | 想不到新地方 | 基于位置发现周边没去过的好店 |

---

## 🤔 为什么不直接用大众点评或高德？

| | 大众点评 | 高德地图 | Date Spot |
|:---|:---|:---|:---|
| 排序逻辑 | 热度/评分 | 距离 | 风格匹配 + 距离 + 多样性 |
| 筛选 | 需要手动选分类 | 显示所有 POI | 自动排除火锅/KTV/快餐 |
| 两人中点 | 不支持 | 不支持 | 自动算中点 + 双方通勤时间 |
| 天气 | 不考虑 | 不考虑 | 下雨自动推室内 |
| 营业时间 | 显示但不筛选 | 不筛选 | 自动标注状态，已关门降权 |
| 约人闭环 | 没有 | 没有 | 选点 → 导航 → 生成邀请消息 |

简单说：大众点评告诉你"哪家店评分高"，高德告诉你"附近有什么"，Date Spot 告诉你"你们俩去哪最合适"。

---

## ⚙️ 技术亮点

| 特性 | 说明 |
|:---|:---|
| 高德 Web Service API | 6 类 POI 分别搜索，智能排除（火锅、KTV、快餐） |
| 双人通勤计算 | 路径规划 API 分别计算双方到达时间，评估公平性 |
| 天气联动 | 天气 API 自动判断，雨天不推荐户外 |
| 高德深链接 | 每个推荐附 `uri.amap.com` 导航链接，点击直达高德 App |
| 地图模式 | JS API v2.0 + AMap.Walking 路径规划，移动端优先 |
| 对话流闭环 | 不满意 → 追问原因 → 重新推荐，支持 POI 详情查询 |

---

## 🚀 快速开始

### 安装

```bash
openclaw skills install @dongdongyue/amap-date-spot
```

### 环境变量

| 变量名 | 必填 | 获取方式 |
|--------|------|----------|
| `AMAP_API_KEY` | ✅ | [高德开放平台](https://lbs.amap.com/) → 控制台 → 添加 Key → 类型选「Web 服务」 |
| `AMAP_JSAPI_KEY` | ❌ | 同上，类型选「Web端(JS API)」，用于交互地图 |
| `AMAP_SECURITY_JS_CODE` | ❌ | JS API 安全密钥 |

> 免费额度：5000 次/天。

### 使用

在 AI 助手中直接说：

```
帮我找个约会的地方，在新街口附近
```

```
我在大行宫，她在河西万达，第一次见面
```

```
找个安静的咖啡馆，适合谈事情
```

```
都不喜欢，有没有公园可以散步的
```

---

## 📂 示例

两个真实场景，基于高德 API 实时数据生成：

| 场景 | 模式 | 动线 | 文件 |
|------|------|------|------|
| 🍲 百家湖·咖啡→火锅→清吧 | ☕→🍲→🍷 三站 | 星巴克→左庭右院→PEACE PANDA | [`examples/baijiahu-hotpot-bar/`](examples/baijiahu-hotpot-bar/) |
| 🎬 九龙湖+建邺万达·西餐→电影→清吧 | 🍽️→🎬→🍷 双人 | 乐班→幸福蓝海→PLUTO | [`examples/jiulonghu-wanda/`](examples/jiulonghu-wanda/) |

每个示例包含：
- `report.md` — 完整推荐 + 动线 + 行为指南 + API 原始数据
- `map.html` — 决策地图（给自己看：评分/备选/行为指南）
- `invitation.html` — 邀请卡片（发给 ta：干净请帖风格）
- `date_plan.csv` — 行程 CSV

---

## 📂 项目结构

```
amap-date-spot/
├── README.md                      # 本文件
├── SKILL.md                       # Skill 定义（核心）
├── skill.json                     # 元数据
├── LICENSE                        # MIT 协议
├── docs/                          # 效果截图
│   ├── screenshot-map.png
│   ├── mobile-map-link.jpg
│   └── mobile-map-invitation.jpg
├── .env.example
├── .gitignore
├── references/
│   ├── invitation-card.html       # 邀请卡模板（4主题色·copy-paste可用）
│   ├── html-template-map.md       # 决策地图模板（InfoWindow+安全区+多路线）
│   ├── text-card-date-spot.md     # CSS 降级卡片（无 JS Key 时）
│   └── text-card-template.md      # 纯文本输出格式
├── examples/
│   ├── baijiahu-hotpot-bar/       # ☕→🍲→🍷 咖啡+火锅+清吧
│   │   ├── report.md
│   │   ├── map.html               # 决策地图
│   │   ├── invitation.html        # 邀请卡片
│   │   └── date_plan.csv
│   └── jiulonghu-wanda/           # 🍽️→🎬→🍷 西餐+电影+清吧（双人）
│       ├── report.md
│       ├── map.html
│       ├── invitation.html
│       └── date_plan.csv
```

### 调用的高德 API

| API | 用途 |
|-----|------|
| `geocode/geo` | 地名 → 坐标 |
| `place/around` | 周边 POI 搜索 |
| `direction/transit/integrated` | 公交路线 |
| `direction/walking` | 步行路线 |
| `weather/weatherInfo` | 天气查询 |

---

## 📄 License

MIT

---

<div align="center">

## 🌐 One Sentence Pitch

> **The only AI skill that plans your entire date — finds the spot, builds the itinerary, and generates a shareable invitation card you can send directly to them.**

## 🌐 Scenario

> Xiaolin finally asked a girl from the neighboring class to meet up.
>
> She's at Hexi Wanda, he's at Daxinggong. They agreed to meet somewhere in between. **But where?**
>
> He said one sentence: **"I'm at Daxinggong, she's at Hexi Wanda, find us somewhere in the middle — first date"**

Date Spot found a lakeside café, 4 minutes walk from the midpoint, with a navigation link.

### What it does

- **Smart style inference**: Detects your intent from keywords (romantic / casual / artsy / business)
- **Dual-location midpoint**: Geocodes both locations, calculates midpoint, searches nearby
- **Commute fairness**: Shows how long each person needs to travel
- **Weather-aware**: Won't recommend parks on rainy days
- **Deep links**: Every venue comes with an Amap navigation link
- **Interactive map mode**: Optional HTML map with walking routes (AMap JS API v2.0)

### Install

```bash
openclaw skills install @dongdongyue/amap-date-spot
```

> Requires a free Amap API Key. See [Environment Variables](#environment-variables).

### Environment Variables

| Variable | Required | How to get it |
|----------|----------|---------------|
| `AMAP_API_KEY` | ✅ | [Amap Open Platform](https://lbs.amap.com/) → Console → Add Key → type: 「Web Service」 |
| `AMAP_JSAPI_KEY` | ❌ | Same, type: 「Web(JS API)」 — for interactive maps |
| `AMAP_SECURITY_JS_CODE` | ❌ | JS API security code |

> Free tier: 5,000 calls/day.

### Usage

```
Find us a date spot near Xinjiekou, Nanjing
```

```
I'm at Daxinggong, she's at Hexi Wanda — first date
```

### FAQ

**Q: What if I don't like the recommendations?**
Just say "too expensive" or "anything closer?" — the assistant will adjust and recommend 3 new places.

**Q: Which cities are supported?**
All cities in China with Amap POI data. Weather integration works nationwide.

**Q: Do I need to install Python?**
No. This Skill is pure prompt-driven — the AI assistant calls Amap's HTTP API directly.

</div>
