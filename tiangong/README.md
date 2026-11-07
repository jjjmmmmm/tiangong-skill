# tiangong · 天工

把一套产品开发流程与开发纪律法典化为 skill：agent 在开发时遵从这套开发手册推进。

## 名字由来

明宋应星著《天工开物》，收录农工百艺之法，图说并重，使后人按图可循、依法可造。本 skill 取"天工"为名：开发如开物——先明法度，后施巧艺；不靠灵感，按工序。

## 结构

```text
tiangong/
├── SKILL.md          总纲：触发条件、五条总纲、任务四要素、九阶段总览与路由、增补与新一轮迭代、跨阶段纪律、本地 skill 调度衔接
├── references/       九阶段细则（进入该阶段时按需阅读）
│   ├── 01-inception.md        立项与需求规格
│   ├── 02-structure.md        组成与技术选型
│   ├── 03-contracts.md        数据与调用约定
│   ├── 04-kickoff.md          工程起步
│   ├── 05-main-path.md        主路径贯通与可演示
│   ├── 06-core-advance.md     核心推进
│   ├── 07-integration-debug.md 贯通验证与排错
│   ├── 08-delivery.md         验证与交付准备
│   └── 09-retrospective.md    结项复盘与大报告
└── templates/        十五份工件骨架
    ├── CONSTITUTION.md       项目宪法（本项目不变铁律）
    ├── charter.md            立项书
    ├── requirements.md       需求规格
    ├── architecture.md       架构说明（模块职责表+选型比选表）
    ├── api-contract.md       接口约定
    ├── PROJECT_MEMO.md       项目备忘
    ├── master-plan.md        总计划（放 docs/plan/PLAN.md，每次为一步）
    ├── session-plan.md       按次计划（放 docs/plan/<步骤号>.md）
    ├── devlog.md             开发日志（按次追加）
    ├── demo.md               演示说明
    ├── gaps.md               差距清单（放入 docs/gaps.md）
    ├── smoke.md              通检表
    ├── acceptance.md         验收自测表（含安全清单）
    ├── readme.md             README 骨架（放仓库根，对应阶段四）
    └── final-report.md       结项报告
```

## 触发方式

仅显式调用：用户说"按天工来""按天工流程开发""按手册开发""按流程开发"，或点名立项书、需求规格、通检表等手册工件。开始新项目或有多个步骤的任务**不会**自动加载本 skill；用户说"不用走流程了"时只保留四要素、排错五项、安全最低集。

## 安装

把整个 `tiangong/` 目录复制到用户级 skills 目录即全局生效（ZCode 等遵循 `.agents/skills` 约定的工具为 `~/.agents/skills/tiangong/`，Claude Code 为 `~/.claude/skills/tiangong/`）；或放到某项目的 `.agents/skills/` 下仅对该项目生效。

## 试运行建议

用这几个提示词测试触发与流程是否符合预期：

1. "我要做一个新项目：在线评测网站，按天工流程开始。"（应从阶段一起步，产出立项书与需求规格草稿）
2. "接口报 500 了，帮我修。"（应先要求排错五项，先定故障层次再改代码）
3. "把剩下功能都做完。"（应拒绝一次性生成，按差距清单拆四要素小步任务）
4. "不用走流程了，直接改。"（应停止阶段推进，仅保留四要素、排错五项、安全最低集）
