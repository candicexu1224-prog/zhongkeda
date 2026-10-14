# d2d-context · 中国科学技术大学化学专业知识图谱

- 设计链接: https://www.figma.com/design/xOHFg28WFNodS09XLii57p/?node-id=80-1042
- fileKey: xOHFg28WFNodS09XLii57p ; 根节点 80:1042 (页面 1920×6802)
- lastModified: 2026-10-14T06:42:55Z
- 切图: /Users/xuxiaoyi/Downloads/中国科学技术大学/切图
- 演示: /Users/xuxiaoyi/Downloads/中国科学技术大学/演示 (server root = 中国科学技术大学)

## 模块骨架（bbox 归零到页面原点）
| # | 模块 | 节点 | bbox | 背景 | 内容来源 |
|---|---|---|---|---|---|
|1|首屏|80:1043|0,0,1920,960|video cover|切图首屏-内容 + AI-cut nav/left/title/right|
|2|培养目标与毕业要求|80:1214|0,960,1920,1258|#FFF|切图标题+内容 + AI-cut texture/details|
|3|支撑矩阵|80:1287|0,2218,1920,927|#FFF|切图内容 + AI-cut header|
|4|专业课程整体框架|80:1401|0,3145,1920,1043|grad #F2F4F7(0/58%)→#FFF|切图内容 + AI-cut header/tabs|
|5|专业方向专题|80:1513|0,4188,1920,1284|#FFF|切图内容(整卡)|
|6|课程知识图谱|80:1589|0,5472,1920,1054|grad #FFF→#EDEFF2 + texture|切图内容 + AI-cut texture/header/tabs|
|7|底部|80:1617|0,6526,1920,276|切图整卡|切图底部|

## 装配规格（module-local 1x）
M1 h960: video inset0 | hero-nav(0,0,w1920) | hero-left(215,318.2,w173) | hero-title(603,220,w730) | 首屏-内容(468,220,w1000) | hero-right(1548,317.2,w158)
  首屏-内容定位: 切图 alpha 全宽扫描 card top=222(display); 树 card 80:1110 top=442 → top=220(=80:1101 top), left=468, w=1000
M2 h1258: m2-texture(0,0,w1258) | 标题(120,80,w1680) | 内容(120,217,w1680) | m2-details(120,1154,w1680)
M3 h927: m3-header(120,40,w1680) | 内容(120,167,w1680)
M4 h1043: m4-header(120,70,w1680) | m4-tabs(120,207,w770) | 内容(120,300,w1680)
M5 h1284: 内容(20,20,w1880)
M6 h1054: m6-texture(0,0,w1920) | m6-header(120,60,w1680) | m6-tabs(120,187,w1680) | 内容(120,270,w1680)
M7 h276: 底部(0,0,w1920)

## 执行观测
- 模块分级: M1 代码参与; M2~M7 纯拼装
- 漏切(AI 补切 12 张): hero nav/left/title/right, m2 texture/details, m3 header, m4 header/tabs, m6 texture/header/tabs
- M4 渐变实测: y100~600≈#F2F4F7 平台→1000 到 #FFF

## 验收（?static=1 全页截图 1920×6802，逐模块 crop.py diff scale=1）
- m2 1.152 LOW / m3 0.076 LOW / m4 0.513 LOW / m5 0.819 LOW / m6 3.543 LOW / m7 0.837 LOW
- m1 整模块 DIFF（视频帧差异，属动态豁免）；不透明前景 glass-card 区域 diff=1.989 通过；left/right/nav 为半透明叠视频，残差来自视频帧非布局
- m2 内容切图含阴影出血(3373×1804 vs 节点3360×1794)：alpha 实心区在画布 (3,0)→(1682.5,896.5)，故按 left=117,top=217,width=1686.5 落位（树节点 120,217,1680,897 + 出血补偿）；修复前 mean 4.97→修复后 1.152

## 更新轮（Figma lastModified 07:20）
- 导航右上名字设计稿已改为【进入空间】(Alibaba PuHuiTi 3.0 700 16px)，重渲染 hero-nav.png 生效，截图核验通过
- 切图内容更新（尺寸不变）：专业方向专题-内容.png、底部.png；演示直接引用切图路径自动生效
- 因设计变动全量重渲染 12 张 AI-cut + 重下 7 张模块参照；模块 bbox 未变，落位不变
- 复测 diff：m2 1.152 / m3 0.076 / m4 0.513 / m5 0.785 / m6 3.543 / m7 0.841 全 LOW

## 首屏数据卡改代码活写（弃切图）
- 删除 assets/hero-left.png、hero-right.png；改为 .statcol/.stat 活写 + 毛玻璃
- 参数全取树：列 left/top/width=215,318.2,173 与 1548,317.2,158；gap10；卡 r16、pad18/20/18/16、高94(93)；icon22；label PingFang 500 15/21；num Avenir 900 22/30 ls.44 斜体；unit 15/21 opacity.8 margin-top6
- 背景模糊：Figma BACKGROUND_BLUR radius50 → backdrop-filter:blur(25px)（含 -webkit- 前缀）；底色 rgba(0,0,0,0.38)（参照采样内部≈视频×0.7 定标）
- 8 个图标 AI 渲染 2x：assets/stat-icon1..8.png（44×44）
- 几何为树值结构保证：label x=263/1596、num y=363.2/362.2、unit y=369.2/368.2 均与树一致

## 进入空间 下拉菜单（树 91:3838）
- 活写按钮覆盖导航烘焙按钮：(1763,24,117,46) r12，linear-gradient(90deg,#2C83F8,#5253FB)，pad 12/16/12/20，gap6，文字 Alibaba PuHuiTi 3.0 700 16/22 #FFF + CSS caret（开合旋转180°）
- 菜单：top=按钮下4px、right 对齐按钮右缘(1880)、宽167、r8、shadow 0 2px 12px rgba(0,0,0,.10)、pad 8/0；3 项 62 高 pad10/20 gap2；标题 500 16/22 #474D59、副题 400 13/18 #7E838C；hover 项 #EDF3FF + #266FFF（=设计中的选中态样式）
- 交互：hover 展开 + 点击开合 + 外部点击关闭；展开淡入+上移6px .22s；?dd=1 为验收常开钩子
- 字体内嵌：fonts/AlibabaPuHuiTi-3-{55-Regular,65-Medium,85-Bold}.ttf（本机 mdfind 命中拷入），@font-face 400/500/700
- 几何核验：菜单 left=1713/top=74/right=1880，按钮 left=1763，与树一致

## 替换 培养目标与毕业要求-内容 切图（15:35 新文件）
- 新文件尺寸/出血与旧版一致（canvas 3373×1804，实心区 3.0→1682.5 / 0→896.5）→ 落位不变 left=117,top=217,width=1686.5
- 重下参照 80:1214（设计 07:38 变动）复测 m2 diff=1.154 LOW，像素一致

## 进入空间 箭头修正（按设计完全还原）
- 弃 CSS 手绘 chevron；改渲染设计矢量 I91:3783;3228:868（线性/上箭头）2x → assets/dd-caret.png（12×12，墨迹 11×6.5 ≈ 树 10.7×6.2）
- 定位取树：按钮内 left:89/top:17（=caret 实例 bbox 139,17 减按钮原点 50,0）；收起 rotate(180deg) 朝下、展开 rotate(0) 朝上，.25s 过渡
- 截图比对开/合两态与 ref-91-3838 按钮：形状/粗细/位置一致

## 二次替换 培养目标与毕业要求-内容 切图（15:40 新文件）
- 尺寸/出血仍一致（3373×1804，实心区 3.0→1682.5 / 0→896.5）→ 落位不变
- 重下参照 80:1214（设计 07:43 变动）复测 m2 diff=1.155 LOW

## 入场动效改为可逆（每次滚到都播放）
- IO 不再 unobserve：isIntersecting 时加 .reveal、离开视口（rootMargin -6% 盒外）移除 .reveal 复位
- revealCheck 兜底改为对称 toggle（top<94%vh 且 bottom>0 才保持）
- ?static=1 验收模式不受影响（STATIC 时不 toggle，CSS 强制全显）
- 验证：load 仅 m1；#m5 时 m1 复位+m5 播放；回 #m1 重新播放

## 底部(m7)入场只播一次
- m7 加 class="once"；IO/revealCheck 中 once 模块显现后写 dataset.done=1，滚出视口不再移除 .reveal（锁定）
- 其余模块保持可逆
- 序列实测（滚到底→回顶）：m2~m6 复位 hidden，m7 保持 REVEAL；临时 seq 钩子验证后已移除

## 发布（GitHub + Cloudflare）
- 演示目录自包含化：切图拷入 演示/切图（index.html 路径改为 切图/）；refs/shots 移至 ../verify/（不入仓库/不入部署）
- git：演示目录 init -b main，首提交 34 文件（含切图/字体/资产，~65MB）；安全审查按用户选择跳过
- Cloudflare：wrangler assets-only Worker `ustc-chem-graph`（配置 qoder/wrangler.ustc-chem.jsonc，assets.directory=/tmp/ustc-deploy 干净副本 32 文件无点文件）
  URL: https://ustc-chem-graph.chaoxing.workers.dev ；沙箱 curl workers.dev 超时（网络限制），需用户浏览器目视
- GitHub：待用户提供空仓库 URL 后配置 remote；推送需代理 git -c http.proxy=http://127.0.0.1:7897 -c https.proxy=http://127.0.0.1:7897 push -u origin main
- GitHub 远程已配置并推送成功：https://github.com/candicexu1224-prog/zhongkeda.git （main，09cc6d6；钥匙串凭证+代理 7897）

## 首屏中部改活写（弃 首屏-内容/hero-title 切图）
- 标题活写：Alibaba PuHuiTi 3.0 900 80px ls12.8，渐变字 linear-gradient(180deg,#FFF 59%,rgba(255,255,255,.8))（handles 垂直）；字体补 105-Heavy.woff2
- 副标题活写：D-DIN Exp 400（本机 /Users/xuxiaoyi/Library/Fonts/D-DINExp.otf 内嵌），— 22px ls1.76 + 中句 16px ls3.04 + —，flex 居中 gap10
- 玻璃卡活写：80:1111 rgba(0,0,0,0.2)（paint opacity 0.2）+ backdrop-filter blur(9.9px)（BACKGROUND_BLUR 19.8 减半）+ inset 0 0 78.1px rgba(2,0,99,.25) + r32；下半 80:1116 横向黑渐变 a.045→.3（paint opacity .3 × stops .15→1）+ blur(10.55px)（21.1 减半）+ r32
- 问候语活写 PingFang 500 22/26 ls1.32 @ (696,470.6)
- 头像 AI 渲染 80:1115 2x → assets/hero-avatar.png @ (535,374,150)
- 仅对话框用切图：首屏-对话框.png (1914×360→957×180 无出血) @ (489.6,543.6)
- 核验：白面板像素边 ref/shot 左顶右完全一致(492/545/1444)；残差 mean≈4 集中在 chips 行=切图(08:12UTC)早于设计(08:14:34UTC)约2分钟所致，非落位问题
- 删除 assets/hero-title.png、切图/首屏-内容.png（演示内副本）
- 坑：补丁曾弄坏 Regular 字体行 url 引号致整表 CSS 崩坏（页面塌缩），已修复

## 玻璃卡描边 + 三块底对齐（设计 08:26）
- 描边按树 strokes：80:1111 border:1.6px solid rgba(255,255,255,0.25)（paint opacity .25, INSIDE）；80:1116 border:1.2px solid rgba(255,255,255,0.3)；对话框描边已烘焙在切图内
- 底对齐 y=745.2：左列 top 318.2→340.2、右列 317.2→339.2（中部不变，card 底 745.2）
- 与 08:26 新参照并排核对一致

## 边框圆角细节 + 数据卡描边（设计 08:27）
- 玻璃卡 80:1111 圆角 32→34；描边维持 1.6px rgba(255,255,255,.25)
- 数据卡新增内描边（树 strokes）：左列 1px rgba(0,0,0,0.25)、右列 1.6px rgba(0,0,0,0.25)，.statcol.left/.right 区分
- 对话框描边(#DADEE8 1px)/圆角24 已烘焙切图内，未变
- 与 08:27 新参照并排核对一致

## 边框再更新 + 首页胶囊效果（设计 08:39）
- 数据卡描边统一 1.6px rgba(0,0,0,0.25)（左列由 1px 改 1.6px，与右列一致）
- 玻璃卡描边 alpha .25→.20；下半 .30→.20；圆角 34 维持
- 首页胶囊：重渲染 hero-nav.png 生效（RADIAL 白 a.8→a.2 × paint opacity .30 + 1px 白@10% 内描边 + GLASS 效果）
- 按钮箭头改渲染导航实例 I91:3753;3228:868（下箭头 @70%）：闭合 rotate(0) 朝下、展开 rotate(180) 朝上；开/合截图核验通过

## 数据卡描边改白色（修正误读）
- 树 strokes 为双 paint：[0] 白色渐变描边 visible:false（禁用），[1] SOLID #FFF paint opacity 0.15（生效）
- 之前误取 strokes[0]（GRADIENT 无 color 字段→被读成 #000）做成黑描边；修正为 border:1.6px solid rgba(255,255,255,0.15)
- 截图核对白色细描边与参照一致

## 首屏背景视频换压缩版
- video src 改为 切图/首屏-背景视频-压缩.mp4（940KB，原 3.0MB；时长约 8.06s）；拷贝进 演示/切图/ 并删除旧副本 首屏-背景视频.mp4
- 核验：HTTP 200 全量 940650 字节；headless 截图首帧正常渲染，首屏各活写层不受影响

## 首屏视频再换：首屏视频高清-压缩.mp4
- 设计师目录旧两个视频已移除，仅剩 首屏视频高清-压缩.mp4（3.2MB）；拷贝进 演示/切图/ 并改 video src，删除 首屏-背景视频-压缩.mp4 副本
- 核验：HTTP 200 全量 3231644 字节；截图首帧高清渲染正常

## Cloudflare 二次部署（含全部首屏迭代）
- 重建 /tmp/ustc-deploy（index.html+assets+fonts+切图，45MB 无点文件）后 wrangler deploy：8 新文件/26 缓存，Version dc58474e-4b78-4fb9-a876-659467226f8b
- URL 不变 https://ustc-chem-graph.chaoxing.workers.dev ；沙箱 curl 不通 workers.dev，用户浏览器目视
- GitHub 仍 @09cc6d6（本轮仅部署未推送）

## GitHub Pages 国内镜像（无域名方案）
- 原因：workers.dev 在中国大陆被 DNS 污染/阻断；账号下无 zone 且用户无域名 → 自定义域名不可行
- 推送 main 09cc6d6..b2b6dfe；API 启用 Pages（source main / 根目录）；status built
- 镜像 URL: https://candicexu1224-prog.github.io/zhongkeda/ （首页 200 标题正确；中文路径视频 200 全量）
- Cloudflare 版本并存：https://ustc-chem-graph.chaoxing.workers.dev （VPN/海外）

## 首屏加载优化（视频空窗）
- 根因：3.2MB 视频首帧到达前 video 透明露白底
- 方案：① m1 加深色底 #071725 防白闪；② video 加 poster=assets/hero-poster.jpg（headless 抽视频首帧转 JPEG q72，84KB）即时占位；③ preload="auto" 提前下载
- 验证：?static=1 + virtual-time-budget=200 截图首屏已为完整深色画面（poster 生效），无空白期

## 视频三换：首屏视频高清叠化-压缩.mp4
- 3.67MB；拷贝进 演示/切图/、改 video src、删除 首屏视频高清-压缩.mp4 副本
- poster 重抽为新视频首帧（79KB JPEG），早期加载截图确认占位画面完整无白屏
