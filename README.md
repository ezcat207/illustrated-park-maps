# illustrated-park-maps

Stroly 风格的手绘旅行地图：给国家公园做的插画风旅行图。

## 双层架构

- **Step 1 · 插画层（纯 HTML）**：单文件 HTML + 内联 SVG，手绘质感的地图；
  推荐 / 次推荐景点画成二维插画投影在地图上，点击看介绍卡。静态、离线可看。
- **Step 2 · 实时地图层（Leaflet）**：免费开源的 Leaflet + 免费底图，
  同一套 POI 数据以插画 marker 落在真实地图上；GPS 实时显示用户位置；
  点击景点 → 一键跳 Google Maps 导航。

参考例子：stroly.com 插画观光地图（实测该站本身就是基于 Leaflet 构建的——
用户说的"免费的地图"就是 Leaflet）。

## 第一个公园

大峡谷国家公园（Grand Canyon National Park）→ `parks/grand-canyon/`

## 目录

- `docs/SPEC.md` — 产品规格（用户流程、数据模型、两步范围与验收）
- `docs/TASKS.md` — 任务拆解
- `data/grand-canyon-pois.json` — 大峡谷 POI 数据（14 个点：8 推荐 + 6 次推荐）
- `parks/grand-canyon/index.html` — Step 1 插画版（T3）
- `parks/grand-canyon/map.html` — Step 2 实时版（T4）
