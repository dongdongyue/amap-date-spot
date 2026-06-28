# 决策地图 HTML 模板（给自己看）

全屏地图 + 底部抽屉面板 + 点击 Marker 弹出信息窗。移动端优先，iPhone 安全区适配。

## 模板

```html
<!DOCTYPE html><html lang="zh-CN"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover"><title>{标题}</title><style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overflow:hidden}
body{font-family:-apple-system,'PingFang SC','Microsoft YaHei',sans-serif;background:#f0f2f5}
#map{width:100%;height:100%}
.bottom-sheet{position:fixed;left:0;right:0;bottom:0;z-index:1000;background:#fff;border-radius:16px 16px 0 0;box-shadow:0 -2px 16px rgba(0,0,0,.08);max-height:42vh;overflow-y:auto;padding:0 16px max(16px,env(safe-area-inset-bottom,16px))}
.bottom-sheet::before{content:'';display:block;width:36px;height:4px;border-radius:2px;background:#e0e0e0;margin:10px auto 8px}
.venue-card{display:flex;align-items:flex-start;gap:12px;padding:14px;margin-bottom:8px;border-radius:14px;background:#fafafa;cursor:pointer;transition:background .15s;min-height:44px}
.venue-card:active{background:#f0f0f0}.venue-card.active{border:2px solid #1890ff;background:#e6f7ff}
.venue-dot{width:14px;height:14px;border-radius:50%;flex-shrink:0;margin-top:4px}
.venue-info{flex:1;min-width:0}.venue-name{font-size:14px;font-weight:600;color:#1a1a1a;margin-bottom:2px}
.venue-meta{font-size:11px;color:#999;line-height:1.6}.venue-reason{font-size:12px;color:#555;margin-top:4px;line-height:1.5}.venue-backup{font-size:10px;color:#bbb;margin-top:3px}
.map-header{position:fixed;top:max(12px,env(safe-area-inset-top,12px));left:16px;z-index:999;background:rgba(255,255,255,.94);backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);padding:8px 16px;border-radius:12px;font-size:13px;font-weight:700;color:#1a1a1a;box-shadow:0 1px 4px rgba(0,0,0,.06)}
.route-legend{position:fixed;bottom:calc(42vh + 16px);right:12px;z-index:999;background:rgba(255,255,255,.92);border-radius:10px;padding:8px 12px;font-size:10px;color:#666;box-shadow:0 1px 6px rgba(0,0,0,.08);display:flex;flex-direction:column;gap:4px}
</style></head><body>
<div class="map-header">{地图头部}</div><div id="map"></div>
<div class="route-legend"><span>实线=到推荐点</span><span style="color:#FF6B8A">虚线=动线</span><span>👆 点击标记看详情</span></div>
<div class="bottom-sheet" id="sheet">
{VENUE_CARDS}
</div>
<script>
var p=new URLSearchParams(location.search);
var K=p.get('key')||'{AMAP_JSAPI_KEY}';
var S=p.get('security')||'{AMAP_SECURITY_JS_CODE}';
window._AMapSecurityConfig={securityJsCode:S};
var C=[{lng},{lat}];
var V=[{VENUES_ARRAY}]; // [{lng,lat,name,emoji,desc,style}]
var CO={romantic:'#FF6B8A',casual:'#4ECDC4',artsy:'#A78BFA',business:'#64748B'};
var map=null,walkers=[],infoWin=null;
function focusVenue(i){var v=V[i];if(map){map.setCenter([v.lng,v.lat]);map.setZoom(16)}document.querySelectorAll('.venue-card').forEach(function(c){c.classList.remove('active')});var card=document.getElementById('c'+i);if(card){card.classList.add('active');card.scrollIntoView({behavior:'smooth',block:'nearest'})}}
function navTo(v){window.open('https://uri.amap.com/navigation?to='+v.lng+','+v.lat+','+encodeURIComponent(v.name)+'&mode=car&coordinate=gaode','_blank')}
</script>
<script src="https://webapi.amap.com/loader.js"></script>
<script>
AMapLoader.load({key:K,version:'2.0',plugins:['AMap.Walking']}).then(function(AMap){
  map=new AMap.Map('map',{center:C,zoom:15,viewMode:'2D'});
  infoWin=new AMap.InfoWindow({offset:new AMap.Pixel(0,-50),closeWhenClickMap:true});
  new AMap.Marker({position:C,map:map,zIndex:100,content:'<div style="background:#64748B;color:white;padding:6px 14px;border-radius:14px;font-size:14px;font-weight:700;white-space:nowrap;box-shadow:0 2px 10px rgba(0,0,0,.25)">📍 {区域名}</div>'});
  V.forEach(function(v,i){
    var mk=new AMap.Marker({position:[v.lng,v.lat],map:map,zIndex:90+i,content:'<div style="background:'+CO[v.style]+';color:white;padding:5px 10px;border-radius:10px;font-size:13px;font-weight:600;white-space:nowrap;box-shadow:0 2px 8px rgba(0,0,0,.2);cursor:pointer">'+(i+1)+'. '+v.emoji+' '+v.name+'</div>'});
    mk.on('click',function(){infoWin.setContent('<div style="padding:4px 0"><b style="font-size:14px">'+v.emoji+' '+v.name+'</b><p style="font-size:12px;color:#666;margin:6px 0">'+v.desc+'</p><a href="javascript:void(0)" onclick="navTo(V['+i+'])" style="display:inline-block;padding:6px 14px;background:#1890ff;color:white;border-radius:8px;font-size:12px;text-decoration:none;margin-top:4px">🧭 导航到这里</a></div>');infoWin.open(map,mk.getPosition())});
    var w=new AMap.Walking({map:map,hideMarkers:true});walkers.push(w);w.search(new AMap.LngLat(C[0],C[1]),new AMap.LngLat(v.lng,v.lat));
  });
  new AMap.Polyline({map:map,path:V.map(function(v){return[v.lng,v.lat]}),strokeColor:'#FF6B8A',strokeWeight:3,strokeOpacity:.55,strokeStyle:'dashed',strokeDasharray:[10,6],showDir:true,zIndex:5});
  map.setFitView(null,false,[70,70,70,60]);
});
</script>
</body></html>
```

## 替换清单

| 占位符 | 说明 |
|--------|------|
| `{AMAP_JSAPI_KEY}` | 环境变量，支持 `?key=` URL 参数覆盖 |
| `{AMAP_SECURITY_JS_CODE}` | 同上，`?security=` URL 参数覆盖 |
| `{lng},{lat}` | 会面点坐标 |
| `{VENUES_ARRAY}` | `[{lng,lat,name,emoji,desc,style},...]` — 按推荐顺序 |
| `{VENUE_CARDS}` | 底部卡片 HTML，每张 `<div class="venue-card" onclick="focusVenue(i)" id="ci">...` |
| `{区域名}` | 会面区域名 |
| `{地图头部}` | 如 "📍 新街口 · ☕ 下午茶" |

## 交互功能

- **点击 Marker** → 弹出 InfoWindow（店名 + 描述 + 🧭 导航按钮），点击按钮跳转高德 App
- **点击底部卡片** → 地图聚焦 + 卡片高亮
- **Walking 路线** → 每个推荐点独立 AMap.Walking 实例，不会被覆盖
- **动线虚线** → Polyline 串联所有推荐点，带方向箭头
- **右下角图例** → 实线/虚线/点击提示
- **手机安全区** → `safe-area-inset-*` 适配刘海屏/Home Indicator
