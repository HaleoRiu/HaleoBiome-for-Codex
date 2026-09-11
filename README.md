# HaleoBiome for Codex / ChatGPT

基于 Haleo 的 [HaleoBiome](https://github.com/HaleoRiu/HaleoBiome) 设计，由 Supervisor、Planner、Analyzer、Inspector、Visual Reviewer 根据知识库、用户问题和实际数据共同完成微生物组下游分析。

这是面向 Codex / ChatGPT 的指令型 Skill。分析代码由 Analyzer 在项目运行时生成；不附带固定分析管线。支持扩增子、宏基因组等数据，具体分析范围和输入约定由研究问题与数据语义确定。

## 安装与调用

Skill 目录为 [`skills/haleobiome`](skills/haleobiome)。在能够访问本私有仓库的 Codex 中请求：

```text
使用 skill-installer 安装 https://github.com/HaleoRiu/HaleoBiome-for-Codex/tree/main/skills/haleobiome
```

也可把完整 `haleobiome` 目录放入宿主的个人 skills 目录。本次本机安装位置为 `~/.codex/skills/haleobiome`；其他版本的发现路径以宿主指引为准，不重复安装到多个扫描位置。

调用示例：

```text
用 HaleoBiome 分析这个目录的宏基因组数据。
我的问题是治疗相关的物种与通路变化，受试者有重复测量。
请先清点输入、审查环境，并提交包含方法依据和未做事项的分析计划。
```

Codex 可通过 `$haleobiome` 或 Skill 选择器调用；支持独立 Skill 的 ChatGPT 桌面环境可从 Skills 中选择。该格式由两个产品共享，但本机安装不等于已经向其他设备或 ChatGPT 网页账户分发。[官方 Skill 文档](https://learn.chatgpt.com/docs/build-skills)说明了独立 Skill 与插件分发的范围；需要跨网页/移动端分发时可另行打包插件。

## 行为

- Supervisor 将核心知识库与用户指定领域扩展、运行时文献核验结合；Planner 按数据、设计和用户要求形成方案。
- 不预设分组数、环境变量、软件语言、模型、分析模块或文献数量。
- 方案确认后生成和运行代码；Analyzer 运行期间 Inspector 独立审查并即时反馈，修订产生新版本。
- 图就绪后数值复核与视觉审查并行；Supervisor 终审有证据支持的结论。
- 探索/验证取向、依赖安装和范围只确认尚未授权的事项；技术修复沿用批准方案。
- 角色按可用槽位分阶段调度，不要求五个同时运行。真正并行需要宿主提供子代理、后台执行和消息工具；不能以单助手角色扮演冒充五个独立 Agent。缺失执行/读图能力会明确报告。

## 文件

- `skills/haleobiome/SKILL.md`：动态规划与执行入口。
- `references/`（Skill 内）：角色交接、运行协议、规划提示、核心知识地图。
- `agents/openai.yaml`（Skill 内）：名称、说明与默认调用提示。
- `VALIDATION.md`：结构及行为验证范围。

领域扩展从用户指定路径按需读取；不自动收集或上传本机研究资料。分析输入、生成代码和结果写入用户项目目录，不写入 Skill 安装目录。

## 来源与许可

原设计：Haleo；原 OpenClaw 实现：OpenClaw；此版本的宿主适配：Codex，按 Haleo 要求制作（2026-09-11）。核心知识地图继承原仓库并明确条件化使用规则，文献与具体方法仍需在任务中核验。

保留上游 MIT 许可证及 Haleo 的著作权声明，见 [LICENSE](LICENSE)。私有仓库用于独立维护平台适配版本。
