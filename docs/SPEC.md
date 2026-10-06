# 产品规格：Illustrated Park Maps（插画旅行地图）v0.2

日期：2026-10-06 ｜ 状态：v0.2（T1 坐标核实、T4 Leaflet 实时版已完成）｜ 第一个公园：大峡谷国家公园

## 1. 背景与参考

参考例子：stroly.com 的插画观光地图（viewer/1760424216，志贺岛文化财地图）——
二维景点插画投影在地图上，点击查看。

实测发现：该例子本身就是基于 **Leaflet**（免费开源地图库）构建的。
用户说的"免费的地图"（Leaflet）即为本项目的 Step 2 技术选型。

## 2. 产品定义：双层架构

| | Step 1 插画层 | Step 2 实时地图层 |
|---|---|---|
| 形态 | 单文件 HTML，内联 SVG 手绘风地图 | Leaflet + 免费底图（Carto Positron / OSM） |
| POI 呈现 | 二维插画投影在手绘地图上 | 同一套 POI 数据，插画 marker 落在真实地图上 |
| 用户位置 | 无（示意） | GPS 实时蓝点 + 精度圈 |
| 点击景点 | 介绍卡 | 介绍卡 → 一键 Google Maps 导航 |
| 网络 | 离线可看 | 需在线（底图瓦片 + GPS） |

两层共用同一套 POI 数据（`data/grand-canyon-pois.json`），插画资产复用。

## 3. 用户流程

1. 用户打开地图（插画版 / 实时版可互相切换）。
2. 在实时版上看到自己的实时位置（蓝点）。
3. 浏览二维插画景点：★ 推荐景点用大插画，次推荐用小插画，一眼区分。
4. 点击景点 → 弹出介绍卡（中英双语、一句话亮点）。
5. 点"导航" → 跳 Google Maps App/网页：
   `https://www.google.com/maps/dir/?api=1&destination={lat},{lng}`
   点"在地图上看" → 切到 Leaflet 实时图并平移到该点。

## 4. POI 分级

- `recommended`（推荐）：必看。大插画 marker。首批 8 个。
- `secondary`（次推荐）：顺路看。小插画 marker。首批 6 个。

## 5. 数据模型（data/grand-canyon-pois.json）

```json
{
  "id": "mather-point",
  "name_zh": "马瑟点",
  "name_en": "Mather Point",
  "lat": 35.9953, "lng": -111.9988,
  "tier": "recommended",
  "category": "viewpoint",
  "blurb_zh": "南缘最经典的日出观景点…",
  "blurb_en": "…",
  "verified": false
}
```

- `category`: viewpoint（观景点）/ trailhead（步道口）/ hub（集散）
  / lodge（住宿餐饮）/ cultural（人文）
- `verified=false` 表示坐标待核实（T1），Step 2 上线前必须全部 true。

## 6. Step 1 范围与验收（T3）

- 单文件 `parks/grand-canyon/index.html`：内联 SVG + CSS + JS，无构建步骤，双击即看。
- 大峡谷南缘手绘风：峡谷示意 + 14 个景点插画 marker + 图例（推荐/次推荐）+ 点击弹窗。
- 中英双语切换。
- 验收：14 个点全可点、弹窗信息与 POI 数据一致、手机浏览器布局不错乱。

## 7. Step 2 范围与验收（T4）

- `parks/grand-canyon/map.html`：Leaflet 1.9 + Carto 免费底图，divIcon 复用 Step 1 插画 SVG。
- `navigator.geolocation.watchPosition` 实时蓝点 + 精度圈（需 HTTPS 或 localhost）。
- 详情卡两个按钮：Google Maps 导航 / 回到插画版。
- 验收：真机 GPS 蓝点跟随移动、导航链接坐标正确、弱网有 loading 态。

## 8. 非目标（v0.1 不做）

离线地图包、原生 App、用户账号/收藏同步、多公园切换 UI（T6 再做）。

## 9. 待定 / 风险

- T1 坐标核实完成前，Step 2 不锁数据。
- 插画风格定稿需用户过目（先发 HTML 给用户看，改完再定）。
- Leaflet 底图 tile 用量：Carto 免费档个人项目够用，流量起来后评估自建。
