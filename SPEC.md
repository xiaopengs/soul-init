# 🧬 灵魂生成器 — Soul Initializer

> 给新 Agent 初始化灵魂的选择界面。从技能卡片到灵魂特质，组装你的第一只龙虾。

---

## 1. Concept & Vision

一个仪式感十足的"灵魂组装台"。用户像在组装一台精密机器一样，从技能库和灵魂特质库中挑选组件，卡片会以优雅的动画飞入中央的机器人容器，最终生成一套完整的初始化命令。

**感觉：** 科幻操作台 + 炼金术士的工作台。暗色系 + 琥珀金光晕，有深度的交互。

---

## 2. Design Language

**Aesthetic:** 科幻控制台 — 深邃暗色背景 + 琥珀金色强调 + 霓虹光晕边缘

**Color Palette:**
- Background: `#09090f`
- Surface: `#12121c`
- Card: `#1a1a28`
- Border: `rgba(245, 158, 11, 0.15)`
- Amber Primary: `#f59e0b`
- Amber Glow: `rgba(245, 158, 11, 0.25)`
- Text Primary: `#f4f4f5`
- Text Secondary: `#9ca3af`
- Accent Blue: `#3b82f6`
- Accent Purple: `#a78bfa`
- Accent Green: `#22c55e`

**Typography:**
- Headings: Inter, weight 700-800
- Body: Inter, weight 400-500
- Code/Mono: JetBrains Mono

**Motion:**
- Card selection: scale up 1.05 + border glow pulse + float animation
- Card to container: FLIP animation — card shrinks and translates to container
- Container activation: pulse glow when cards arrive
- Stagger: cards appear with 50ms stagger delay
- Ambient: subtle floating particles in background

---

## 3. Layout & Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  Header: "灵魂生成器" + 副标题                                     │
├────────────────────┬────────────────────┬───────────────────────┤
│                    │                    │                        │
│   技能卡片区        │   机器人容器        │   灵魂特质区            │
│   (Skill Cards)    │   (Robot)         │   (Soul Traits)        │
│                    │                    │                        │
│   可滚动网格        │   3D 机器人        │   可滚动网格             │
│   分类筛选          │   接收飞入卡片      │   分类筛选               │
│                    │   显示已选计数      │                        │
├────────────────────┴────────────────────┴───────────────────────┤
│  预览/导出面板（可折叠）                                          │
│  生成命令 + 复制按钮                                              │
└─────────────────────────────────────────────────────────────────┘
```

**Responsive:**
- Desktop (>1024px): 3-column layout
- Tablet (768-1024px): Robot on top, cards below in 2 columns
- Mobile (<768px): Single column stack

---

## 4. Features & Interactions

### 4.1 技能卡片 (Skill Cards)

**数据来源：** 预置热门技能列表（clawhub 真实数据）

**卡片信息：**
- 技能图标（emoji）
- 技能名称
- 技能描述（1行）
- 分类标签

**交互：**
- Hover: 卡片微微上浮 + 边框发光
- Click: 选中状态（持续发光 + 飞向容器动画）
- 再次点击: 取消选中（卡片从容器飞回原位）

**分类筛选：** 全部 / 开发 / 工具 / 效率 / AI

### 4.2 灵魂特质卡片 (Soul Trait Cards)

**特质列表（预置）：**

| 特质 | 描述 | 分类 |
|------|------|------|
| 第一性原理 | 追问本质，从根因出发 | 思维方式 |
| 严谨客观 | 论点必须有据，不臆断 | 思维方式 |
| 系统思维 | 整体视角，考虑要素关联 | 思维方式 |
| 跨界迁移 | 跨领域类比，激发创新 | 思维方式 |
| 刨根问底 | 不满足表面答案，深挖三层 | 工作风格 |
| 批判性思维 | 质疑假设，审视证据 | 工作风格 |
| 简洁表达 | 复杂问题，简单说清 | 表达风格 |
| 有温度 | 理解情感，不冷冰冰 | 交互风格 |
| 结构化 | 逻辑清晰，层次分明 | 表达风格 |
| 主动预见 | 不只响应，还能预判 | 工作风格 |

**交互：** 同技能卡片

### 4.3 机器人容器 (Robot Container)

- 居中显示，有轻微悬浮动画
- 接收卡片时：发出脉冲光晕
- 顶部显示已选技能数和特质数
- 点击容器：展开/收起已选卡片列表
- 空状态：显示虚线轮廓 + 提示文字

### 4.4 预览/导出面板

**内容：**
```bash
# 技能安装命令
clawhub install github
clawhub install weather

# 灵魂特质初始化
# SOUL.md 追加内容
```

**交互：**
- Tab 切换：命令预览 / 代码预览
- 一键复制
- 下载配置文件（SOUL.md + TOOLS.md）
- 刷新预览（重新生成命令）

---

## 5. Component Inventory

### 5.1 SkillCard
- Default: 暗色卡片 + 边框
- Hover: 浮起 + 边框发光
- Selected: 持续发光 + 打勾标记 + 缩放 1.02
- Disabled: 灰度 + 不可点击

### 5.2 TraitCard
- 同 SkillCard 状态

### 5.3 RobotContainer
- Idle: 轻微悬浮 + 暗色轮廓
- Active (有卡片): 脉冲光晕
- Full (卡片已满): 边框变金色

### 5.4 ExportPanel
- Collapsed: 只显示 "已选 N 项" 条
- Expanded: 完整命令面板

### 5.5 CategoryFilter
- Pill 样式按钮
- Active: 琥珀色背景
- Inactive: 暗色背景 + 边框

---

## 6. Technical Approach

- **纯静态页面**: HTML + CSS + Vanilla JS（无框架）
- **动画**: CSS Transitions + Web Animations API
- **无外部依赖**: 所有功能自包含
- **数据**: 内置 JSON（预置技能和特质数据）
- **导出**: 生成纯文本命令，可复制/下载

---

## 7. 内置技能数据

基于 ClawHub 真实热门技能（2024年数据）:

**开发类:**
- github, github-trending-stable, gh-issues
- weather, healthcheck
- multi-search-engine-simple

**工具类:**
- 1panel-skills, mcporter
- tmux, node-connect

**效率类:**
- self-improving-agent, taskflow
- skill-creator

（完整列表见 index.html 内置数据）
