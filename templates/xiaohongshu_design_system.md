# 小红书图文设计规范 — Design System

> 本文件定义了企业研究小红书图文的统一设计风格。
> 后续调研新公司时，直接复用本规范 + HTML模板，保证全系列视觉一致。

---

## 1. 尺寸与格式

| 项目 | 规格 |
|------|------|
| 单页尺寸 | 1080 × 1080 px（正方形） |
| 总页数 | 15-18页 |
| 输出格式 | HTML渲染 → 浏览器截屏为PNG |
| 截屏方式 | Chrome DevTools → 选中 `.page` → 右键 "Capture node screenshot" |

---

## 2. 配色方案

```
背景底色:     #0a0a23 → #0f1a3a → #0d1230（三色渐变，145deg）
标题金色:     #d4af37
正文白色:     #ffffff
弱化文字:     rgba(255,255,255,0.55)
极弱化文字:   rgba(255,255,255,0.3)

强调色-红:    #ff453a / #ff6b6b（警告、风险、不推荐）
强调色-绿:    #34c759（推荐、优势、确认）
强调色-蓝:    #3282f6（信息、中性数据）
强调色-紫:    #af52de（品牌、特殊标注）
强调色-橙:    #ff9f0a（次要分类）

卡片背景:     rgba(255,255,255,0.04)
卡片边框:     rgba(212,175,55,0.15)
高亮框背景:   rgba(212,175,55,0.12) → rgba(212,175,55,0.04)（渐变）
高亮框边框:   rgba(212,175,55,0.35)
```

---

## 3. 字体

```css
font-family: 'Noto Sans SC', 'Microsoft YaHei', sans-serif;
```

引入方式（HTML head）：
```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;600;700;900&display=swap" rel="stylesheet">
```

| 元素 | 字号 | 字重 | 颜色 |
|------|------|------|------|
| 页面主标题 | 48px | 900 | #d4af37 |
| 封面主标题 | 52px | 900 | #d4af37 |
| 副标题 | 22px | 400 | rgba(255,255,255,0.55) |
| 卡片正文 | 23px | 400 | #fff |
| 卡片强调 | 23px | 700 | #d4af37 |
| 高亮框文字 | 24px | 700 | #d4af37 |
| 页码 | 26px | 700 | rgba(212,175,55,0.55) |
| 数据大数字 | 36px | 900 | #d4af37 |
| 评分超大字 | 56px | 900 | #d4af37 |
| 底部提示 | 18-20px | 400 | rgba(255,255,255,0.3) |

---

## 4. 布局规则

### 4.1 页面结构
```
┌──────────────────────────────┐
│                    页码 NN/NN │  ← 右上角
│                              │
│  主标题（金色大字）            │
│  副标题（灰色小字）            │
│                              │
│  ┌──────────────────────┐    │
│  │ 卡片 1               │    │
│  └──────────────────────┘    │
│  ┌──────────────────────┐    │
│  │ 卡片 2               │    │
│  └──────────────────────┘    │
│  ...                         │
│                              │
│  ┌──────────────────────┐    │
│  │ 高亮总结框            │    │  ← 底部收尾
│  └──────────────────────┘    │
└──────────────────────────────┘
```

### 4.2 内边距
- 页面内边距: 52px 56px 48px 56px（上右下左）

### 4.3 卡片
- 圆角: 14px
- 内边距: 20px 24px
- 间距: 14px（卡片之间）
- 左侧有一个 38×38px 的彩色圆角图标

### 4.4 背景装饰
- 右上角: 400px 的微弱金色径向渐变光斑
- 左下角: 300px 的微弱蓝色径向渐变光斑
- 不使用任何背景图片，纯CSS实现

---

## 5. 图标规则

**禁止使用 emoji**（浏览器截屏时经常渲染为方块）。

替代方案：用 CSS 彩色圆角方块 + HTML实体字符：

| 用途 | 字符 | HTML实体 |
|------|------|----------|
| 推荐/确认 | ✔ | `&#10004;` |
| 不推荐 | ✘ | `&#10008;` |
| 五角星 | ★ | `&#9733;` |
| 圆点 | ● | `&#9679;` |
| 三角 | ▲ | `&#9650;` |
| 菱形 | ◆ | `&#9670;` |
| 箭头 | ➔ | `&#10132;` |
| 三角播放 | ► | `&#9658;` |
| 警告 | ! | 字母 `!` |
| 分类标识 | 首字母 | 如 S/M/V/B/R/L |

图标容器样式：
```css
.icon {
  width: 38px; height: 38px;
  border-radius: 10px;
  display: flex; align-items: center; justify-content: center;
  font-size: 18px; font-weight: 900;
}
```

---

## 6. 组件清单

| 组件 | CSS类名 | 用途 |
|------|---------|------|
| 信息卡片 | `.card` | 每条信息的标准容器 |
| 高亮框(金) | `.highlight` | 每页底部的总结语 |
| 高亮框(红) | `.highlight.highlight-warn` | 风险/警告总结 |
| 高亮框(绿) | `.highlight.highlight-green` | 推荐/优势总结 |
| 高亮框(灰) | `.highlight.highlight-neutral` | 中性建议 |
| 两列对比 | `.two-col` + `.col-red` / `.col-green` | WLB等对比 |
| 阶梯图 | `.stair` + `.stair-step` | 薪资/晋升的递进展示 |
| 对比表格 | `.compare-table` | 竞品对比 |
| 评分表格 | `.score-table` | 各维度评分 |
| 数据卡片 | `.stat-grid` + `.stat-card` | 封面大数字展示 |
| 行动项 | `.action` + `.action-r/y/g` | 投递建议的优先级标注 |
| 最终评价 | `.final-box` + `.rating` | 总评分大框 |

---

## 7. 18页标准结构

| 页码 | 主题 | 主要组件 |
|------|------|----------|
| 01 | 封面 | stat-grid（4宫格大数字） |
| 02 | 一句话认识 | highlight（核心定位）+ card列表 |
| 03 | 核心业务 | 2×3 grid 的 card |
| 04 | 行业位置 | compare-table |
| 05 | 为什么值得关注 | card列表（5条优势） |
| 06 | 应届生岗位 | 分组card（理系/文理） |
| 07 | 适合什么背景 | card列表 + highlight-warn |
| 08 | 招聘流程 | stair（选考漏斗） |
| 09 | 薪资福利 | stair（年收阶梯）+ card |
| 10 | 地点与路径 | card + stair（クラス制） |
| 11 | 企业文化/WLB | two-col（红绿对比） |
| 12 | 最强的点 | card列表（5条） |
| 13 | 最大的风险 | card列表（warn边框） |
| 14 | 适合投的人 | card列表（green边框） |
| 15 | 不适合投的人 | card列表（warn边框） |
| 16 | 整体评价 | score-table + final-box |
| 17 | 投递建议 | action（红/黄/绿优先级） |
| 18 | 总结 | final-box + 文字段落 |

---

## 8. 快速复用指令

对新公司生成小红书图文时，使用以下 prompt：

> 请参考 `templates/xiaohongshu_design_system.md` 中的设计规范，
> 为 [公司名] 生成一个完整的18页小红书HTML文件。
>
> 要求：
> - 每页1080×1080px，统一深蓝底+金色标题的设计风格
> - 不使用emoji，使用HTML实体字符+CSS图标
> - 使用 Noto Sans SC 字体
> - 参考 `companies/keyence/assets/xiaohongshu/all_pages.html` 的CSS结构
> - 输出到 `companies/[公司名]/assets/xiaohongshu/all_pages.html`
>
> 内容来源：`companies/[公司名]/` 下的研究文件。

---

## 9. 参考文件

- 完整CSS源码：`companies/keyence/assets/xiaohongshu/all_pages.html`
- Keyence成品效果：`companies/keyence/assets/xiaohongshu/page_01.png` ~ `page_18.png`
