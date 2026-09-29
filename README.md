# Vibe Coding Skill Pack

一套开箱即用的 Codex 开发工作流：需求确认 → UI Demo → TDD → 文档同步 → 代码审查，装完就能让 AI 按纪律写代码。

## 这是什么

让 Codex 按你的规矩写代码。内置需求复述确认、UI Demo 可视化确认、TDD 强制流程、文档与代码同步、迭代复盘机制。新项目一条命令创建，AI 不会跳步、不会丢上下文、不会改你计划外的文件。

## 安装

1. clone 本仓库
2. 在 Codex 里打开 clone 下来的目录
3. 对 Codex 说："帮我安装这套工作流"
4. Codex 会读取 setup/INSTALL.md 自动执行安装步骤

## 包含内容

| 组件 | 作用 |
|------|------|
| AGENTS.md | 主控硬规则（路由、流程门控、Demo 规则、复述确认） |
| core-dev skill | 文档规范、版本管理、迭代复盘 |
| planning-with-files skill | 长任务外挂记忆（task_plan / findings / progress） |
| ui-ux-pro-max skill | UI 设计资源库（79 种风格、192 套配色、119 条 UX 规则） |
| .templates | 新建项目模板（AGENTS.md、docs、demos） |
| setup/INSTALL.md | 自动化安装指南 |

## 依赖

- [Superpowers 插件](https://github.com/obra/superpowers)（通过 Codex 插件市场安装，提供 TDD/调试/验证/审查/Git 流程）