# 任务拆解

规格见 `docs/SPEC.md`。每步完成标准：用户过目点头（插画类）或真机验证通过（地图类）。

- [x] **T0** 建仓 + SPEC + 任务拆解（2026-10-06）
- [ ] **T1** POI 坐标核实：14 个点逐个搜索核实 lat/lng，`verified` 全置 true
- [ ] **T2** 插画资产：5 类 SVG icon（viewpoint / trailhead / hub / lodge / cultural）
      × 推荐/次推荐两档尺寸，风格统一
- [x] **T3** Step 1：`parks/grand-canyon/index.html`（单文件插画地图，SPEC §6）(2026-10-06)
- [ ] **T4** Step 2：`parks/grand-canyon/map.html`（Leaflet 实时地图，SPEC §7）
- [ ] **T5** 真机 GPS 实测（iPhone 上开 map.html：蓝点、导航跳转）
- [ ] **T6** 模板化：第二个公园复用同一套管线（POI json + 两套 HTML 模板）
