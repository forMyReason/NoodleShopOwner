# NoodleShopOwner 🍜

把任意公司的市值缩放成 **100 块**，用「极具犀利商业眼光的面馆老板」的视角读财报：家底几斤两、一年净赚净亏、家底打工效率如何，多公司横比一眼看出哪家值得盘、哪家是陷阱。

> **免责声明**：本框架为估值透视与财报解读工具，**非投资建议**。数据以指定报告期与市场来源为准，Agent 在关键字段缺失时会停损，不会编造数字。

---

## 为什么需要 100 块法？

市值从几亿到几万亿，直接对比 PE/PB 很难建立直觉。100 块法做一件事：

**把所有公司统一缩放到「市值 = 100 块」**，再算：

| 步骤 | 面馆语言 | 公式 |
| :--- | :--- | :--- |
| 1 锚定 | 盘店开价 | **100 块** |
| 2 家底 | 账面净资产 | **100 ÷ PB** |
| 3 利润 | 过去一年赚/亏 | **PE > 0**：`100 ÷ PE`（TTM）<br>**亏损**：`(净利润_TTM ÷ 实际总市值) × 100` |
| 4 ROE | 家底打工效率 | **利润 ÷ 净资产**（100 块口径） |

苹果 PB 40、腾讯 PB 3.9——数字差 10 倍，体感不对。换成 100 块口径：苹果家底 2.48 块、腾讯 25.64 块，立刻看出「轻资产印钞机」和「中资产稳增长」是两种完全不同的店。

---

## 功能亮点

- **单公司 / 多公司**：单店深度解读，或多店终极对比表 + 核心洞察 + 老板一句话
- **面馆语言翻译**：拒绝「PE 合理、建议关注」套话，输出可执行的判断句
- **亏损路径**：PE ≤ 0 或 TTM 亏损时禁止 `100 ÷ PE`，走市值缩放，标注「无效（亏损）」
- **停损机制**：关键字段缺失只报已采数据 + 缺失清单，不下终极结论
- **验算脚本**：附 Python 脚本，盈利 / 亏损路径均可本地验算

---

## 安装

### 方式一：作为项目 Skill（推荐）

克隆本仓库到你的项目根目录，或把 `NoodleShopOwner/` 复制到目标项目的 `.cursor/skills/` 下：

```bash
git clone https://github.com/forMyReason/NoodleShopOwner.git
# 或将 skill 目录复制到已有项目：
# cp -r NoodleShopOwner  your-project/.cursor/skills/NoodleShopOwner
```

Cursor 会自动加载项目级 Skill。

### 方式二：全局 Skill

复制到 Cursor 用户目录，所有项目可用：

```bash
# macOS / Linux
cp -r NoodleShopOwner ~/.cursor/skills/NoodleShopOwner

# Windows（PowerShell）
Copy-Item -Recurse NoodleShopOwner $env:USERPROFILE\.cursor\skills\NoodleShopOwner
```

### 依赖

- [Cursor](https://cursor.com) IDE（支持 Agent Skills）
- Agent 需联网（通过 WebSearch / WebFetch 获取财报数据）
- 验算脚本：Python 3.10+（仅 `NoodleShopOwner/scripts/calc_anchor.py`，无第三方依赖）

---

## 使用

在 Cursor Agent 对话中，用自然语言触发即可。常见触发词：

- `@NoodleShopOwner`
- 「100 块法」「估值归一化透视法」「面馆类比」
- 「对比苹果和腾讯」「哪家更值得盘」「PE/PB/ROE 对比」

### 示例提问

```
帮我用 100 块法对比分析苹果和腾讯 2025 年财报
```

```
@NoodleShopOwner 分析一下比亚迪，报告期用最新年报
```

Agent 会按四步 SOP 搜集数据、计算、输出面馆语言解读。完整输出示例见 [examples.md](NoodleShopOwner/examples.md)（苹果 vs 腾讯双公司演示）。

---

## 验算脚本

目录：`NoodleShopOwner/scripts/calc_anchor.py`

```bash
# 盈利公司
python NoodleShopOwner/scripts/calc_anchor.py --pb 35.22 --pe 40.4

# 亏损公司（市值缩放路径）
python NoodleShopOwner/scripts/calc_anchor.py \
  --pb 0.33 --net-profit-ttm -59.52 --market-cap 365.08

# 内置自检
python NoodleShopOwner/scripts/calc_anchor.py --self-check
```

输出示例：

```
net_assets_100=2.4752
profit_100=2.4844
roe_100=100.37%
```

---

## 项目结构

```
NoodleShopOwner/              # 仓库根
├── README.md
├── LICENSE
└── NoodleShopOwner/          # Skill 内容（安装时复制到 .cursor/skills/NoodleShopOwner/）
    ├── SKILL.md              # Skill 主入口：路由、SOP、停损规则、自检清单
    ├── reference.md          # 公式细则、边界情况、输出模板
    ├── examples.md           # 苹果 vs 腾讯完整双公司演示
    └── scripts/
        └── calc_anchor.py    # 100 块法验算（stdlib only）
```

| 文件 | 说明 |
| :--- | :--- |
| [SKILL.md](NoodleShopOwner/SKILL.md) | Agent 行为定义与工作流程 |
| [reference.md](NoodleShopOwner/reference.md) | 术语映射、亏损路径、盘店检查清单 |
| [examples.md](NoodleShopOwner/examples.md) | 标准输出结构与话术参考 |

---

## 输出长什么样？

单公司：核心数据表 → 100 块面馆表 → 反直觉洞察 → 风险信号 → 老板一句话。

多公司额外包含：

```
## 终极对比：N 家「面馆」排排坐

| 面馆 | 市值 | 过去1年利润 | 账面家底 | PE | PB | ROE | 你的评价 |
```

「你的评价」列要求判断句，例如「几乎无家底，但赚钱能力极强，靠品牌和生态」——不是复读 PE/PB 裸数字。

---

## 贡献

欢迎 Issue 和 Pull Request：公式边界、话术模板、新行业解读（金融股、周期股等）、验算脚本增强。

提 Issue 时请附上：公司名/代码、报告期、期望输出 vs 实际输出。

---

## 许可证

本项目采用 [MIT License](LICENSE) 开源。使用前请阅读 Skill 内的免责声明——工具归工具，投资决策归你自己。

---

## 相关概念

- **100 块法 / 市值锚定法 / 估值归一化透视法**：同一方法论的不同叫法
- **面馆类比**：把市值、净资产、净利润、ROE 映射为盘店开价、家底、年赚年亏、家底回报率

如果这个项目帮你看懂了一家「面馆」，Star ⭐ 一下，让更多老板学会盘店。
