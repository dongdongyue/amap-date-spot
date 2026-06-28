# 约会地点推荐 - CSS 文字卡片模板

当用户未配置 JS API Key 时，生成此文字卡片作为地图替代。纯 CSS + 数据，无外部依赖，手机友好。

## 完整模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>约会地点推荐 - {区域名}</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: -apple-system, 'PingFang SC', 'Microsoft YaHei', sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh; padding: 16px; color: #333;
  }

  .card {
    background: #fff; border-radius: 16px; padding: 24px;
    margin-bottom: 12px; box-shadow: 0 4px 20px rgba(0,0,0,.1);
  }

  /* 头部 */
  .header { text-align: center; }
  .header h1 { font-size: 22px; margin-bottom: 6px; }
  .header .subtitle { font-size: 13px; color: #999; }
  .header .weather { font-size: 12px; color: #888; margin-top: 4px; }

  /* 推荐卡片 */
  .venue-card {
    display: flex; align-items: flex-start; gap: 14px;
    padding: 18px; border-radius: 14px; margin-bottom: 10px;
    border-left: 5px solid #1890ff;
    transition: transform .15s;
  }
  .venue-card:active { transform: scale(.98); }
  .venue-1 { border-left-color: #FF6B8A; background: #FFF5F7; }
  .venue-2 { border-left-color: #4ECDC4; background: #F5FDFC; }
  .venue-3 { border-left-color: #A78BFA; background: #F9F5FF; }
  .venue-4 { border-left-color: #64748B; background: #F8FAFC; }

  .venue-emoji { font-size: 32px; flex-shrink: 0; line-height: 1; }
  .venue-info { flex: 1; }
  .venue-name { font-size: 17px; font-weight: 700; margin-bottom: 4px; }
  .venue-style {
    display: inline-block; font-size: 10px; padding: 2px 8px;
    border-radius: 10px; font-weight: 600; margin-left: 6px;
    vertical-align: middle;
  }
  .style-romantic { background: #FFE0E6; color: #D94A6A; }
  .style-casual { background: #D4F5F2; color: #2E9E93; }
  .style-artsy { background: #EBE0FF; color: #7B5CE0; }
  .style-business { background: #E2E8F0; color: #475569; }

  .venue-meta { font-size: 13px; color: #666; margin: 6px 0; }
  .venue-meta span { margin-right: 12px; }
  .venue-reason { font-size: 13px; color: #444; margin: 8px 0; }
  .venue-reason::before { content: '✨ '; }

  /* 状态标记 */
  .status-open { color: #52c41a; }
  .status-soon { color: #faad14; }
  .status-closed { color: #ff4d4f; }

  /* 导航按钮 */
  .nav-link {
    display: inline-block; margin-top: 6px; padding: 6px 14px;
    background: #e6f7ff; color: #1890ff; border-radius: 14px;
    font-size: 12px; text-decoration: none; font-weight: 500;
  }
  .nav-link:active { background: #bae7ff; }

  /* 综合推荐 */
  .final-pick {
    background: linear-gradient(135deg, #FF6B8A, #FF8E7A);
    color: #fff; padding: 20px; border-radius: 14px;
    text-align: center;
  }
  .final-pick h3 { font-size: 16px; margin-bottom: 6px; }
  .final-pick p { font-size: 13px; opacity: .9; }

  /* 小贴士 */
  .tips { font-size: 13px; color: #666; line-height: 1.8; }
  .tips .emoji { font-size: 16px; }

  /* 底部 */
  .footer {
    text-align: center; padding: 16px; font-size: 11px;
    color: rgba(255,255,255,.6);
  }
  .footer a { color: rgba(255,255,255,.8); }

  /* 续场建议 */
  .next-spot {
    font-size: 12px; color: #888; margin-top: 6px;
    padding: 6px 10px; background: #fafafa; border-radius: 8px;
  }
  .next-spot::before { content: '➡️ 聊得好？'; margin-right: 4px; }
</style>
</head>
<body>

<!-- 头部 -->
<div class="card header">
  <h1>💕 {地图标题}</h1>
  <p class="subtitle">📍 推荐区域：{区域名}</p>
  <p class="weather">{天气提示}</p>
</div>

<!-- 推荐卡片 -->
<!-- 每个 venue 使用 venue-N 样式，N 为 1-4 对应排名 -->
<div class="venue-card venue-1">
  <div class="venue-emoji">{emoji}</div>
  <div class="venue-info">
    <div class="venue-name">
      {店名}
      <span class="venue-style style-{风格}">{风格标签}</span>
    </div>
    <div class="venue-meta">
      <span>📌 {地址}</span>
      <span>🚶 步行 {X} 分钟</span>
    </div>
    <div class="venue-meta">
      <span class="status-open">🟢 营业中</span>
      <span>💰 人均 ¥{X}</span>
      <!-- 双人模式时显示 -->
      <span>🚶 你 {X}min | 她 {X}min</span>
    </div>
    <div class="venue-reason">{推荐理由}</div>
    <a class="nav-link" href="https://uri.amap.com/marker?position={lng},{lat}&name={encoded_name}" target="_blank">🧭 导航到这儿</a>
    <div class="next-spot">步行 {X} 分钟到 {续场店名}，适合续摊</div>
  </div>
</div>

<!-- 更多 venue 卡片... -->

<!-- 最终推荐 -->
<div class="card final-pick">
  <h3>🏆 如果只选一个</h3>
  <p>选 {店名}——{核心理由}</p>
</div>

<!-- 小贴士 -->
<div class="card tips">
  <span class="emoji">💡</span> <b>小贴士</b><br>
  {场景建议}<br>
  {天气提示细化}<br>
  {破冰话题建议（如适用）}
</div>

<div class="footer">
  由 <a href="https://lbs.amap.com">高德地图</a> 提供数据支持 · Date Spot Skill
</div>

</body>
</html>
```

## 数据注入说明

AI 生成时需替换：

1. **头部** — `{地图标题}`（如"你们的约会地图"）、`{区域名}`、`{天气提示}`
2. **推荐卡片** — 每个推荐一张卡，使用 `venue-1`/`venue-2`/`venue-3` 对应排名的边框颜色
3. **风格标签** — `style-romantic`(浪漫#FF6B8A) / `style-casual`(轻松#4ECDC4) / `style-artsy`(文艺#A78BFA) / `style-business`(商务#64748B)
4. **营业状态** — `status-open`(🟢营业中) / `status-soon`(🟡即将开门) / `status-closed`(🔴已关门)
5. **双人模式** — 有第二个地点时显示通勤时间行，单人或无第二个地点时省略
6. **续场建议** — 每个推荐下方附步行可达的续场地点
7. **导航链接** — `https://uri.amap.com/marker?position={lng},{lat}&name={URL_ENCODED_NAME}`
8. **小贴士** — 包含场景建议、细化天气提示、破冰话题（如"第一次见面"场景）

## 设计特点

- 无需任何外部依赖
- 渐变紫色背景 + 白色卡片
- 左侧彩色边框区分排名（粉→青→紫→灰）
- 风格标签用圆角小徽章展示
- 营业状态颜色编码
- 导航链接点击直达高德地图 App
- 最终推荐区域用渐变暖色卡片突出
