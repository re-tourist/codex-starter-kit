# Codex Project Starter Kit V0

一个用于新项目冷启动的最小模板，让项目尽快进入：

- 文档驱动
- 规则持久化
- Codex 半自动执行
- 人类做高层判断

本模板不追求“全自动开发”，而是追求：

1. 让 Codex 快速理解项目
2. 减少人肉搬运 prompt / feedback
3. 把项目规则沉淀到仓库，而不是聊天记录
4. 让 issue / milestone 可以被稳定执行和审查

---

## Starter Kit 的定位

这是一个 **V0 最小系统**，不是完整自动化平台。

它主要解决：

- 如何让 Codex 快速理解一个新仓库
- 如何在仓库里固定项目规则
- 如何生成最小的计划/issue/审查文档
- 如何建立“你做高层决策，Codex 做执行”的工作流

它暂时不解决：

- 完整 CI 自动化
- 完整多 agent 编排
- 自动 merge / 自动发版
- 所有项目类型的特化模板

---

## 推荐工作流

### Step 1：复制模板骨架
把本模板复制到你的新项目中。

### Step 2：先生成项目快照
使用 `repo-snapshot` skill 扫描仓库，产出：

- `docs/snapshots/project_snapshot.md`

### Step 3：生成项目级 `AGENTS.md`
基于项目快照、README、现有文档，生成项目自己的 `AGENTS.md`。

### Step 4：补项目高层上下文
手动完善：

- `docs/ai/PROJECT_CONTEXT.md`

这一层主要由你负责，因为它承载项目目标、阶段边界和成功标准。

### Step 5：生成 stage / issue 文档
基于项目上下文和当前目标，生成：

- `docs/plan/plan_stageX.md`
- `docs/plan/issue_stageX.md`

### Step 6：进入日常开发
之后，尽量不要再靠长 prompt 解释项目，而是直接让 Codex 读取仓库内文档后执行任务。

示例指令：

- `实现 issue_stage1.md 中的 issue 1.2，先 plan，再实现、验证、更新文档，并调用 reviewer 做初审。`
- `完成 plan_stage2.md 中剩余 scope，遇到 stop conditions 就停止并汇报。`

---

## 目录说明

- `AGENTS.md`：仓库级 agent 工作说明书
- `.codex/config.toml`：项目级 Codex 配置
- `.agents/skills/`：可复用流程能力
- `docs/ai/`：项目高层上下文
- `docs/plan/`：stage / issue 规划
- `docs/review/`：审查规范
- `docs/contracts/`：冻结边界、接口、实验约束
- `docs/handoff/`：里程碑收尾与交接
- `prompts/`：元提示词资产
- `templates/`：模板文件资产

---

## 角色分工

### 你负责
- project goal
- milestone
- contract freeze
- research / product decision
- evaluation design
- 关键结果判读
- 是否继续推进下一阶段

### Codex 负责
- 读取项目规则
- 执行 issue / stage 内实现
- 跑局部验证
- 更新文档
- 输出变更说明
- 做初步 review

---

## 使用原则

1. 优先写仓库文档，不要优先写长 prompt
2. 复杂任务先规划，再编码
3. 默认小步修改，小步验证
4. 先局部验证，再全局验证
5. 研究判断、人类意图、方向转向不要外包给 Codex
6. 高频重复流程，后续再抽成 Skill

---

## 何时升级到 V1

当你在 2 个以上项目中反复使用本模板，并确认以下内容高度重复时，再考虑升级：

- AGENTS.md 模板族
- plan / issue 生成流程
- reviewer 规则
- CI 自动化
- subagents 分工
- 项目类型特化模板

---

## First Real Use

1. 复制本 starter kit 到新项目
2. 让 Codex 使用 repo-snapshot 生成 `docs/snapshots/project_snapshot.md`
3. 基于 project snapshot 生成项目自己的 `AGENTS.md`
4. 人工补全 `docs/ai/PROJECT_CONTEXT.md`
5. 生成人工确认后的 `plan_stage1.md` 和 `issue_stage1.md`
6. 在进入执行前创建 `docs/contracts/contract_freeze_stage1.md`
7. 让 implementer 执行 issue
8. 让 reviewer 做初审
9. 人工只看关键验证、contract 和方向
