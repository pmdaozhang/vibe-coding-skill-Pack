# Vibe Coding 工作区

## 沟通规则

- 全程简体中文，先结论后解释。
- **复述确认**：首次收到新任务描述（2 句话以上）时，回复的第一段必须复述理解，等用户确认后再继续。
- 同一任务的后续补充、简短确认（"好的""继续"）、追问细节时不需要重新复述。

## 执行顺序

1. 复述确认（最先执行，这是 agent 的第一句话）
2. 用户确认后 → 进入项目路由
3. 路由确定项目后 → 调用 Superpowers brainstorming

## 项目路由

收到开发任务时：

1. 用户已指定项目名（如"在 xxx 里..."）→ 进入该子项目，读取其 AGENTS.md
2. 用户没指定但上下文明确 → 确认"当前在 [项目名]，继续？"
3. 无法判断 → 问："这是哪个项目的？"列出已有子项目
4. 项目不存在 → 问："要新建吗？"确认后执行新建流程
5. 每次切换子项目时必须重新读取该项目的 AGENTS.md

## 新建项目流程

用户确认新建后自动执行：

1. 在 vibe coding\ 下创建项目文件夹
2. 进入该文件夹执行 git init
3. 从 .templates\ 拷贝全部模板到新项目
4. 询问技术栈，填写 AGENTS.md 的技术栈和专属规则
5. 更新 vibe coding\.gitignore（把新项目文件夹名加入排除列表）
6. 检查 git 配置（user.name / user.email），未配置则提示用户
7. 汇报"项目已创建，路径是 XXX"

## 中断处理

用户要求新建项目时，如果当前有进行中的开发任务：
1. 先确认"当前 [项目] 有进行中的任务，要先暂停吗？"
2. 用户确认后，将当前进度写入 task_plan.md
3. 再执行新建项目流程

## 新对话恢复

对话开始时，如果用户提到"继续"或任务名：
1. 读 docs/features/ 找对应文档
2. 读 git log 看最后几条 commit
3. 读 task_plan.md（如果有）
4. 向用户确认当前进度后再继续

## 流程分级

### A 级（完整流程）
新功能、架构变更、接口变更、数据模型变更
→ 复述确认 → 路由 → brainstorming（含 Demo 确认）→ 需求文档 → 测试用例 → 计划 → TDD → 验证 → 文档更新 → Code Review → 分支收尾

### B 级（简化流程）
Bug 修复、UI 微调、文案修改
→ 复述确认 → 路由 → systematic-debugging 或直接修改 → 验证 → 更新 CHANGELOG → git commit

### C 级（直接执行）
注释修改、格式化、不改行为的重命名
→ 直接修改，git commit 说清楚

## 文档路径覆盖

Superpowers 的设计文档保存路径覆盖为 docs/features/（不是 docs/superpowers/specs/）。
Superpowers 的实施计划保持默认路径 docs/superpowers/plans/。
测试用例保存到 docs/test-cases/。

## 复杂度升级联动

当 brainstorming 将任务从 Bounded 升级为 Architectural 时，
文档等级自动从 B 级升级为 A 级（补需求文档 + 测试用例）。
禁止降级。

## 文档更新时序

文档更新（CHANGELOG + ROADMAP）是实施计划的任务之一，
必须在 verification 通过后、code review 之前完成。
确保文档变更包含在功能分支的 commit 里。

## 变更纪律

- 只修改计划中列出的文件
- 发现计划外的问题 → 汇报给用户，等用户决定
- 禁止"顺便优化"计划外的文件
- 修改超过 3 个文件时，先列出修改计划等待确认

## 流程门控

写代码前必须满足：
1. 需求已复述并获用户确认
2. 已读目标文件完整内容
3. 已搜索引用关系，描述影响范围
4. 已列出"不修改的文件"清单
5. 有计划且用户批准

汇报"完成"前必须满足：
1. 相关测试已运行且通过
2. UI 变更已按 ui-ux-pro-max 审查
3. 已更新对应文档
4. 已汇报影响范围

## Demo 规则

### 什么时候需要 Demo
新增 UI 组件、修改页面布局、新增页面 → 必须先出 HTML Demo 让用户确认

### 什么时候不需要 Demo
纯逻辑变更、Bug 修复、样式微调 → 直接进 TDD 开发

### Demo 规范
- 存放位置：[项目]/demos/编号-功能名.html
- 独立 HTML 文件，浏览器直接打开
- 内联 CSS，不依赖外部资源
- 展示所有交互状态（正常/hover/active/disabled）
- Demo 是 brainstorming 呈现设计阶段的可视化交付物
- 样式应参考项目现有的主题/设计系统

### Visual Companion vs Demo
- Visual Companion 是 brainstorming 的交互工具，临时使用
- Demo 是设计确认的交付物，保存到 demos/ 目录
- 两者独立，用 Demo 不代表启用了 Visual Companion

## 迭代结束

每完成一次功能迭代或 bug 修复，主动提醒用户：
"要不要做一次复盘？可以更新 skill 规则防止下次再犯。"

## 边界

- 禁止跨子项目读取或修改文件
- 本规则仅适用于 vibe coding 下的子项目
- 用户提到外部项目时，按普通任务处理