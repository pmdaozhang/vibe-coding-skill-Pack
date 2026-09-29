# Vibe Coding 工作流安装指南

你的 Codex 会话如果在 clone 本仓库后打开，请按以下步骤执行安装。
每一步完成后验证结果再进入下一步。

## 前提条件

- Codex 已安装且可正常对话
- git 已安装
- Node.js 已安装（brainstorming Visual Companion 需要）
- Python 3.x 已安装（ui-ux-pro-max 搜索脚本需要）

## 安装步骤

### Step 1: 修改全局 config.toml

文件路径：`~/.codex/config.toml`（Windows 为 `C:\Users\<用户名>\.codex\config.toml`）

找到或创建 `[features]` 段，确保包含以下行：

```toml
[features]
multi_agent = true
```

如果文件中已有 `[features]` 段但没有 `multi_agent`，在段内追加 `multi_agent = true`。
如果 `[features]` 段不存在，在文件末尾追加以上两行。

**验证：** 读取该文件，确认 `multi_agent = true` 存在且只出现一次。

### Step 2: 修改全局 AGENTS.md

文件路径：`~/.codex/AGENTS.md`（Windows 为 `C:\Users\<用户名>\.codex\AGENTS.md`）

在文件末尾追加以下内容：

```markdown
## Skill 适用范围
Superpowers 流程 skill（brainstorming/TDD/调试/验证/审查等）仅在软件开发任务中使用。
写文章、纯问答、内容创作、非代码任务时，忽略 Superpowers 的所有 skill。
```

**验证：** 读取该文件，确认包含"Skill 适用范围"和"忽略 Superpowers"。

### Step 3: 安装 Superpowers 插件

**这一步需要用户在 Codex 界面手动操作，你无法代替执行。**

提示用户：

1. 打开 Codex 应用
2. 点击左侧边栏的 Plugins
3. 搜索 Superpowers
4. 点击安装
5. 重启 Codex

**验证：** 重启后在一个新对话中检查可用 skill 列表，确认 brainstorming、test-driven-development、systematic-debugging 等 skill 已加载。

### Step 4: 确认项目级 skill 已就位

检查当前仓库的 `.codex/skills/` 目录下是否存在以下三个文件夹：

- `core-dev`
- `planning-with-files`
- `ui-ux-pro-max`

如果都在，无需额外操作（Codex 会自动加载项目级 skill）。

**验证：** 逐个读取 `.codex/skills/core-dev/SKILL.md`、`.codex/skills/planning-with-files/SKILL.md`、`.codex/skills/ui-ux-pro-max/SKILL.md` 的 frontmatter，确认格式正确。

### Step 5: 重启 Codex

提示用户重启 Codex 应用，让 config.toml 的 multi_agent 设置生效。

### Step 6: 验证安装

在重启后的新对话中，执行以下测试：

1. 输入"新建一个项目，做个待办事项 APP"
2. 确认 agent 的行为：
   - 第一句话是否复述了你的需求（复述确认规则）
   - 是否询问了技术栈
   - 是否自动创建了项目目录并从 .templates 拷贝了模板
   - 是否触发了 brainstorming skill

如果以上行为全部符合，安装成功。

## 安装后使用

新建项目直接说："新建一个项目，叫 xxx"
开发功能直接说："在 xxx 项目里加一个 xxx 功能"

工作流会自动执行：复述确认 → 路由 → brainstorming → Demo 确认 → 需求文档 → 测试用例 → 计划 → TDD → 验证 → 文档更新 → Code Review → 分支收尾。