# 2026 大蜀道100 · DSD 100K

从大蜀道不夜三国城到昭化古城，沿用户提供的赛事 GPX 查看真实赛道、九站补给、卫星影像、3D 地形与联动海拔剖面。

[打开赛道地图](https://joker-outdoor.github.io/ultra-trail-shudao-2026/) · [Joker Outdoor 路线首页](https://joker-outdoor.github.io/)

页面保留完整模板的全景、俯视、旋转、沿线飞行、统一 / 海拔 / 速度着色、地标点击、剖面联动、手机布局与 2D 降级。`?view=2d` 可直接进入俯视图；本路线没有逐点时间，速度着色不可用。飞行动画与模拟倍速不表示真实运动速度或完赛用时。

## 路线与统计来源

- 坐标与海拔来自用户提供的 2026 大蜀道100赛事 GPX，共 **6151 个原始轨迹点**；按坐标测算的几何距离为 **91.58048005325172 km**（约 91.58 km）。
- 用户提供的赛事站点表公布全程 **92 km**、累计爬升 **3510 m**、累计下降 **3550 m**。页面主里程采用赛事公布距离；地图、飞行进度和海拔剖面的定位仍按 GPX 几何距离计算，两种口径分别保留。
- `route.config.json` 以 `stats.sourceDistanceKm`、`stats.gainM`、`stats.lossM` 和 `statsSource` 记录赛事统计及来源；不将 GPX 海拔噪声累计作为正式爬升。
- 资料海报标注 **26 小时赛事时限**，不代表个人用时。没有个人运动记录、活动日期或可靠时间数据，运动时间与平均配速保持未提供；制作日期为 2026-11-04。
- 九个站点以 GPX 中具名路标的坐标匹配最近赛道点，**不按公布里程比例伪造坐标**。地图站点的几何里程可能与站点表公布里程不同；D5 为换装点。

## 补给站与关门时间

下表里程及关门时间来自**用户提供的赛事站点表**，关门日期均为 **2026 年 11 月 7 日**。未提供关门时间的站点以“—”列示。

| 站点 | 名称 | 公布累计里程 | 关门时间（11 月 7 日） |
| --- | --- | ---: | --- |
| D1 | 普广小学 | 11.4 km | — |
| D2 | 茶园沟 | 17.6 km | 03:00 |
| D3 | 青溪村 | 25.2 km | 05:00 |
| D4 | 钟岭村 | 31.8 km | — |
| D5 | 蜀汉驿站（换装点） | 40.3 km | 09:30 |
| D6 | 翠云廊 | 51.4 km | — |
| D7 | 剑门关南门 | 61 km | 15:00 |
| D8 | 高庙铺 | 71.3 km | 18:00 |
| D9 | 山水人家 | 83.2 km | 21:30 |
| 终点 | 昭化古城 | 92 km | 23:00 |

## 数据与本地预览

`data/` 是本路线的真实公开资产：`route.json`、去除私人元数据的 `route.gpx`、`terrain.json`、全景 `satellite.jpg`，以及 `imagery-detail.json` 和 `imagery-detail/` 近景影像。

全景卫星影像使用 z13，DEM 使用 z12；近景影像使用 z17，共 **196 块**，沿路线按需加载。浏览器读取仓库内资源，无需地图 API key。GPX 海拔用于剖面，3D 路线贴合 DEM；地形高度默认夸张 3 倍，可调回 1 倍。

```sh
python3 -m http.server 8080 --bind 127.0.0.1
```

打开 `http://localhost:8080`。直接打开 HTML 文件不支持 ES modules / fetch。

需要重新生成时，原始赛事 GPX 放仓库外或已忽略的 `inputs/`，使用现有配置和生成器；真实赛道不要使用 `--demo`：

```sh
python3 -m pip install -r requirements.txt
python3 scripts/build_data.py /path/to/original.gpx --config route.config.json --output data
python3 scripts/check_data.py
```

公开 GPX 仅保留轨迹名、坐标和海拔，不含作者、账号、照片、逐点时间及原扩展；公开 JSON 不含逐点绝对时间。

## 本地验证

```sh
npm run check
npm test
```

`examples/fixtures/route.json` 与 `terrain.json` 原样保留自本仓初始基线 `2cdc306aba0aba26b0f91f8ea540e38cf3b469ca` 的合成演示数据，仅供 `scripts/test_city_flight.mjs` 的 `sceneFixture` 默认场景使用，避免赛事路线形状改变既有断言。页面始终读取 `data/`，不会展示这些 fixture。

测试保留模板的飞行、暂停、进度、重播、相机、着色、公里标记、城市几何及近景影像加载 / 失败回退断言；CPU 场景替身不代表 WebGL 画面或手机布局已验收。发布工作流另行完成 review、PR、合入、GitHub Pages 发布与真实 Edge 桌面 / 手机验看。本次不制作 MP4。

## 来源与署名

本次 `app.js` 原样同步共享模板正式 main 的 `7b45e276c7d5e8859b03820f44f5d635c1b0c221`，并同步其线宽回归测试；非城市路线管道半径上限为 3 m，保留短路线原有线宽与城市路线固定线宽。

- 页面由 **Joker Outdoor** 制作，基于[路线可视化模板](https://github.com/joker-outdoor/route-visualization-template)，本仓初始模板基线为 `2cdc306aba0aba26b0f91f8ea540e38cf3b469ca`；模板源自[龙泉七湖连穿](https://github.com/joker-outdoor/longquan-seven-lakes-2026-10-02)，亦参考[贡嘎 100](https://github.com/joker-outdoor/gongga100-2026)。
- 赛道坐标与站点定位：用户提供的赛事 GPX；赛事里程、爬升、下降与关门时间：用户提供的赛事站点表；26 小时时限：用户提供的资料海报。
- Three.js 0.160.0 官方原文件，MIT，见 `vendor/LICENSE`，保留原文。
- 卫星底图：[Esri World Imagery](https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer)。版权归相应影像提供者，不随模板代码再许可；页面保留数据生成器提供的影像署名。
- DEM：[Tilezen / Mapzen Terrain Tiles](https://github.com/tilezen/joerd)，保留[对应数据署名与许可](https://github.com/tilezen/joerd/blob/master/docs/attribution.md)。
