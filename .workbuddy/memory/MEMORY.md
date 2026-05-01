# 孕期管理工具 - 长期记忆

## 项目信息
- **文件**: `/Users/nina/WorkBuddy/20260423152326/pregnancy-tracker.html`
- **桌面分享版**: `/Users/nina/Desktop/孕育时光.html`
- **技术栈**: 纯 HTML + CSS + JS 单文件应用，无框架依赖
- **设计风格**: 温暖粉色系 (pink-400/500/600, cream, lavender)，移动端优先，max-width 480px

## 功能模块 (5个Tab)
1. **首页** - 当周宝宝发育、预警提示、温馨提示
2. **产检** - 产检清单（按周汇总，支持勾选持久化）
3. **菜谱** - 每日菜谱推荐（早餐/午餐/晚餐/加餐），按孕早中晚期推荐不同菜品
4. **时间轴** - 浏览任意孕周详情
5. **体重** - 体重记录与变化追踪

## 数据持久化 (localStorage)
- `pregnancy_lmp` / `pregnancy_edd` - 末次月经/预产期
- `pregnancy_weights` - 体重记录
- `pregnancy_checks` - 产检勾选状态

## 菜谱功能 (2026-04-27 新增)
- 按孕早(4-12周)/中(13-27周)/晚(28-40周)三个阶段分设菜谱库
- 每阶段含早餐7道、午餐7道、晚餐7道、加餐3道
- 每日根据日期种子自动轮换推荐4道菜
- "换一批"按钮可手动刷新
- 每道菜包含：菜名、描述、食材标签、营养亮点
- 底部附当阶段饮食要点提示

## GitHub Pages 部署 (2026-04-28)
- **仓库**: `ninayan8229-gh/pregnancy-tracker`
- **在线地址**: https://ninayan8229-gh.github.io/pregnancy-tracker/
- **本地克隆**: `/tmp/pregnancy-tracker/`（部署用临时目录）
- **gh CLI**: `/tmp/gh-install/gh_2.65.0_macOS_amd64/bin/gh` (v2.65.0)
- 更新流程: 修改源文件 → 复制到 /tmp/pregnancy-tracker/index.html → git push

## Firebase 同步 (已配置)
- 项目: pregnancy-tracker-303d7
- databaseURL: https://pregnancy-tracker-303d7-default-rtdb.asia-southeast1.firebasedatabase.app
- 多房间模式: myRooms [{code, name, role}]，key: pregnancy_rooms / pregnancy_current_room
- 房间支持备注名、创建/加入/切换/退出
- 新用户首次进入后弹出房间引导弹窗（创建/加入/跳过）

## 产检图片上传 (2026-04-28)
- 方案: Canvas 压缩 → Base64 dataURL → 存入 Firebase Realtime Database
- 兼容旧格式: checkedItems 从 true/false 迁移为 {checked, images:[{data, uploadedAt}]}
- 缩略图使用事件委托（data-* 属性），避免 Base64 嵌入 onclick 导致 HTML 解析错误
- 全屏预览弹窗，支持删除

## 自动化
- "孕期每日小贴士推送" - 每天9:00生成当日孕期小贴士
- 存储: `.workbuddy/daily-tips/tip-YYYY-MM-DD.md`
