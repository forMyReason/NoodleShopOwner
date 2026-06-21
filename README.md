# NoodleShopOwner 🍜

用「面馆老板」视角读财报：家底几斤两、一年净赚净亏、家底打工效率如何，多公司横比一眼看出哪家值得盘、哪家是陷阱。



> **免责声明**：估值透视与财报解读工具，**非投资建议**。关键字段缺失时 Agent 停损，不编造数字。



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

在 Agent 对话中 `@noodles-shop-owner`，或说「100 块法」「对比苹果和腾讯」等。示例：

```
帮我用 100 块法对比分析苹果和腾讯 2025 年财报
```

完整输出结构与话术见 [examples.md](noodles-shop-owner/examples.md)。

**100 块法**：统一锚定市值 = 100，算家底 `100÷PB`、利润（盈利 `100÷PE`，亏损走市值缩放）、ROE = 利润÷家底。公式与边界见 [reference.md](noodles-shop-owner/reference.md)。

---

## 文档


| 文件                                                       | 说明                |
| -------------------------------------------------------- | ----------------- |
| [SKILL.md](noodles-shop-owner/SKILL.md)                     | Agent 路由、SOP、停损规则 |
| [reference.md](noodles-shop-owner/reference.md)             | 公式细则、亏损路径、输出模板    |
| [examples.md](noodles-shop-owner/examples.md)               | 苹果 vs 腾讯双公司演示     |
| [calc_anchor.py](noodles-shop-owner/scripts/calc_anchor.py) | 本地验算（stdlib only） |


---

## 贡献

欢迎 Issue / PR。提 Issue 请附公司、报告期、期望 vs 实际输出。

[MIT License](LICENSE)