# NoodleShopOwner 🍜

让 AI **像楼下面馆老板一样说人话**读财报：把 PE/PB/ROE 翻成街坊能懂的话，用 100 块法横比公司，给出盘店直觉（值得盯 / 先别碰 / 家底有毒，**非投资建议**）。

> **免责声明**：估值透视与财报解读工具，**非投资建议**。关键字段缺失时 Agent 停损，不编造数字。

## 适合谁

- 不懂 PE/PB/ROE 的普通读者，想听**大白话**
- 想快速判断一家公司「像不像值得了解的店」
- 需要多公司 100 块口径横比

## 安装

克隆本仓库（GitHub 名 `NoodleShopOwner`，Skill 目录名 `noodles-shop-owner`），将内层 `noodles-shop-owner/` 复制到 `.cursor/skills/noodles-shop-owner/`（项目级）或 `~/.cursor/skills/`（全局）：

```bash
git clone https://github.com/forMyReason/NoodleShopOwner.git
cd NoodleShopOwner
# 复制内层 noodles-shop-owner/（含 SKILL.md）到 skills 目录：

# 全局（macOS / Linux / Git Bash）
cp -r noodles-shop-owner ~/.cursor/skills/noodles-shop-owner

# 全局（Windows PowerShell）
# Copy-Item -Recurse noodles-shop-owner $env:USERPROFILE\.cursor\skills\noodles-shop-owner

# 项目级
# cp -r noodles-shop-owner your-project/.cursor/skills/noodles-shop-owner
```

支持 Cursor / Codex / Claude Code。

验算可选：Python 3.10+，运行 `noodles-shop-owner/scripts/calc_anchor.py --self-check`。

---

## 使用

在 Agent 对话中 `@noodles-shop-owner`，或说「100 块法」「说人话」「对比苹果和腾讯」等。

**小白示例提问：**

```
我是小白，用大白话帮我看看比亚迪值不值得了解
```

**对比示例：**

```
帮我用 100 块法对比分析苹果和腾讯 2025 年财报
```

默认输出顺序：**三句话读懂 → 三个词顺手学 → 100 块表 → 老板拍板 → 原文数字垫底**。

完整输出风格见 [examples.md](noodles-shop-owner/examples.md)（示例一、二为默认；示例三为进阶）。

**100 块法**：统一锚定市值 = 100，算家底 `100÷PB`、利润（盈利 `100÷PE`，亏损走市值缩放）、ROE = 利润÷家底。公式与边界见 [reference.md](noodles-shop-owner/reference.md)。

---

## 文档

| 文件 | 说明 |
| :--- | :--- |
| [SKILL.md](noodles-shop-owner/SKILL.md) | 说人话第一原则、路由、SOP、L0/L1 自检 |
| [reference.md](noodles-shop-owner/reference.md) | 术语强制翻译、盘店裁决、输出模板 |
| [examples.md](noodles-shop-owner/examples.md) | 全人话单公司 + 亏损 + 进阶双公司 |
| [calc_anchor.py](noodles-shop-owner/scripts/calc_anchor.py) | 本地验算（stdlib only） |

---

## 贡献

欢迎 Issue / PR。提 Issue 请附公司、报告期、期望 vs 实际输出。

[MIT License](LICENSE)
