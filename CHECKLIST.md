# 验收清单

## 交付文件

| 文件 | 路径 |
| --- | --- |
| 手机版（原稿未改） | `/workspace/dianshi/bicarbonate-mobile/碳酸氢钠助手-手机版.html` |
| 设计说明 | `/workspace/dianshi/bicarbonate-mobile/DESIGN.md` |
| 本清单 | `/workspace/dianshi/bicarbonate-mobile/CHECKLIST.md` |
| 自动测试脚本 | `/workspace/dianshi/bicarbonate-mobile/test-mobile.mjs` |
| 测试结果 | `/workspace/dianshi/bicarbonate-mobile/test-results.json` |

截图（修复后）：

- 全页：`screenshots/375-assess.png`、`375-dose.png`、`375-safety.png`、`1280-assess.png`、`1280-dose.png`、`1280-safety.png`、`1920-assess.png`、`1920-dose.png`、`1920-safety.png`（目录均为 `/workspace/dianshi/bicarbonate-mobile/`）
- 问题对照：`screenshots/375-tab1-inputs.png`、`375-tab2-dil-select.png`、`375-tab2-dose-panel.png`、`1920-tab1-metrics.png`
- 滚动后导航：`screenshots/375-scrolled-tabs.png`、`1920-scrolled-tabs.png`

## 医学算法

**原样保留，未做医学验算。** 与原版对照测试仍通过（默认值、四个教学病例、自定义输入、清空、剂量/配液控件、配伍药品、核查清单；判读与剂量输出不变）。未改公式、阈值、预设病例值或引用文句。

## 实际浏览器已查范围

- 已查：实际浏览器桌面 1920，以及 DevTools 精确 375 视口。据此修复了双列标签不齐、终体积单位被箭头挡住、桌面指标卡断词、375 粘性页签滚走。
- 未查：真机 Safari（含 iOS 聚焦放大、刘海安全区、真实键盘与滚动）。Android Chrome 真机亦未测。

## 自动测试（Playwright + 系统 Chrome，无登录会话）

54 项全部通过，在原有对照之外补充回归：

- 320 / 375：HCO₃⁻ 与 BE、K⁺ 与 iCa 输入框顶边对齐（误差 ≤1.5px）
- 375：「定容至 500 mL / 250 mL」完整可见，`scrollWidth` 不超过控件宽度
- 1280 / 1920：「代偿」「适当」「蓄积」不被拆到两行；无横向溢出
- 375 / 1920：向下滚动后页签仍为 `position: sticky` 并贴在视口顶部
- `html/body` 的 `overflow-x` 为 `clip`（不是 `hidden`）
- 原有项仍通过：三页签、预设、清空、判读与剂量输出、无 console 错误、320–430 与 1280 无横向溢出、输入 ≥16px、可点区域 ≥48px、无外部请求、无本地存储

## 用户决定移除的功能

- 「复制交班摘要」已从成品中删除（按钮、事件、复制函数、降级复制与交班文本组装），源代码和界面均无该入口。此为用户明确要求，不是隐藏。

## 展示与可用性

- [x] 顶栏不吸顶；瘦页签吸顶，375 滚动后仍留在视口顶部
- [x] 双列长标签换行后输入框对齐，未缩小字号
- [x] 375 目标终体积单位「mL」完整显示
- [x] 桌面指标说明整词保留（呼吸代偿适当、有机酸蓄积）
- [x] 教学病例、机制说明、四大风险默认折叠；剂量、单位、滴速、配液避坑、外渗急救始终可见
- [x] 无 Tailwind CDN，单文件离线
- [x] 无新增教程、额外确认、功能或医学改动

## 限制

- 自动测试在 Linux 无头 Chrome 中进行；真机 Safari 仍未测。
- 「清空重填」范围与原版相同，不会重置第 2 页全部控件。
- 医学内容未经审核，不能当作临床处方依据。
