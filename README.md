# 天工（tiangong）· AI 协作开发手册

> 开发如开物——先明法度，后施巧艺；不靠灵感，按工序。

**tiangong** 是一个给 AI 编程 agent 用的开发流程 skill：把一套九阶段产品开发流程法典化，使 agent 不靠灵感推进项目，而按约定好的工序、交付物与通过标准一步步营造。适用于支持 Agent Skills 的编码工具（ZCode、Claude Code、Gemini CLI、Cursor 等），尤其适合第一次带着 AI 做完整项目的 **vibe coding 新手**（见下文「写给谁」）。

它**只在被点名时生效**：说"按天工来""按手册开发"才加载；日常小修小补、单文件问答不会被打扰。

## 解决什么问题

用 AI 写代码，三种常见死法：

1. **需求没写清就开生成。** 验收全是形容词——"更智能""体验更好"，做完没法判过还是不过。
2. **"把剩下的都做完"。** 一次性生成一大坨，中间某处静默失败，无法定位是哪一步引入的问题。
3. **对话越长，约定越丢。** 早先说好的接口字段，混进后来已作废的结论；换会话、换机器，什么都不剩。

天工的答案：**先约定后生成、一次一小步、一切留痕于仓库。** 需求、结构、接口先写成文档放进 `docs/`，代码按约定生成；选哪道题、边界画在哪、怎样算通过，由人拍板，模型干活。

## 写给谁：vibe coding 新手

天工首先写给**第一次（或前几次）让 AI 帮自己做完整项目的人**。新手不缺模型能力，缺的是三样东西：

- **怎么下任务**——不知道一句需求要拆成"约束、需求、范围、输出"才好验收，于是得到一堆看着完整、无法核对的东西；
- **怎么判完成**——验收全是形容词，做完说不清过还是不过；
- **出了错怎么说**——只会说"不好使"，agent 只能瞎猜。

天工把这三样全部变成模板与话术：说一句"按天工来"，agent 会按九阶段引导你把立项书、验收句、接口约定一项项问出来——你只负责拍板，它负责落成仓库里的文档。每个阶段末有"通过标准"自检，判不出过就不进下一阶段。

带新手的教师与团队负责人可以直接把它当教学与协作的公共工序；有经验的开发者也可以用它把个人习惯固化成 agent 可执行的纪律。

## 它是怎么工作的

对 agent 说一句"**按天工来**"，然后：

1. 它先读仓库里的 `docs/CONSTITUTION.md`（项目铁律）与 `docs/PROJECT_MEMO.md`（约定总汇）——没有就从阶段一起步，先和你把立项书写出来；
2. 按"最早缺失的交付物"定位当前阶段，读对应阶段细则（进度式披露，不占日常上下文）；
3. 把本轮目标拆成**总计划**（`docs/plan/PLAN.md`），每次为一步；轮到哪步，写按次计划（改哪些文件、怎样算对）再动手；
4. 每完成一个可核对的增量就小步提交，自测通过才扩展；结束时更新备忘与开发日志。

## 九阶段

| 阶段 | 关键交付物 | 通过标准 |
|---|---|---|
| 一 立项需求 | 立项书、需求规格（必做/不做、用户故事、验收句） | 每条必做有可按步骤核对的验收句 |
| 二 结构选型 | 架构说明（模块职责表、选型比选表） | 核心需求均有负责模块；说清为何放弃落选方案 |
| 三 数据约定 | 数据模型、接口约定（成功+失败例）、备忘初稿、总计划初稿 | 约定覆盖主路径；假实现已标明 |
| 四 工程起步 | README、.gitignore（逐条说明）、≥3 次小步提交 | 他人可按 README 跑通首跑；改动已通读 |
| 五 主路径贯通 | 端到端主路径、演示说明、差距清单 | 他人可按说明复现主路径 |
| 六 核心推进 | 可独立验证的增量、自测命令、开发日志 | 每块可独立验证 |
| 七 联调排错 | 通检表（≥5 条含 1 条异常）、联调记录 | 通检通过；致命问题当次清零 |
| 八 交付准备 | 回归结果、验收自测表、安全清单 | 重要缺陷清零；自测有结论有凭据 |
| 九 结项复盘 | 完成情况对照表、方案与验证、复盘 | 必做逐条有结论；材料可独立核查 |

阶段可按项目大小压缩或并行，但顺序不可颠倒：约定未定不生成、主路径未通不做细枝、未通读的改动不合入。

## 核心纪律

- **任务四要素**——向 agent 下任何任务前写清：约束、需求、范围、输出；缺一项先补全再动手。
- **形容词不算验收**——验收写成"给定—当—则"，能按步骤判出过或不过。
- **排错五项**——修任何 bug 前写齐：现象、期望、日志原文、相关文件、已尝试；先定故障层次（环境/输入/业务/对接）再改代码。
- **安全最低集**——写进每个任务的约束：仓库与日志无密钥、外部输入服务端校验、登录接口强制鉴权、不与用户字符串直接拼接。
- **假实现三处标明**——临时顶替的固定返回值，在接口约定、代码、备忘三处标明，并写明何时替换。
- **合并纪律**——agent 生成的改动，合入前通读 diff；只写"已审查没问题"不算审查。
- **指令优先**——任何环节与你的指令冲突，一律以你的指令为准。

## 计划：总计划 + 按次计划

不以"天"为单位，以"**次**"为单位。先写总计划，把本轮目标拆成编号步骤，每次只做一步；做之前写按次计划，做完回填。

之后的增补：一步能搞定的小需求，在总计划末尾顺延编号追加即可；要开新一轮迭代或增补量大，就重走一遍九阶段——已有工件（宪法、立项书、备忘……）**不新建、不删除**，只在原文件后面追加，原内容一律保留。

## 安装

把 `tiangong/` 目录复制到你的 skills 目录：

```bash
git clone https://github.com/jjjmmmmm/tiangong-skill.git

# 全局安装（ZCode 等遵循 .agents/skills 约定的工具）
cp -r tiangong-skill/tiangong/ ~/.agents/skills/tiangong/

# Claude Code
cp -r tiangong/ ~/.claude/skills/tiangong/

# 或仅对单个项目生效
cp -r tiangong/ <你的项目>/.agents/skills/tiangong/
```

Windows 下即复制到 `C:\Users\<你>\.agents\skills\tiangong\`。装完说一句"按天工来"验证触发。

## 试一试

1. "我要做一个新项目：在线评测网站，按天工流程开始。"——应从阶段一起步，产出立项书与需求规格草稿
2. "接口报 500 了，帮我修。"——应先要求排错五项，先定故障层次再改代码
3. "把剩下功能都做完。"——应拒绝一次性生成，按差距清单拆四要素小步任务
4. "不用走流程了，直接改。"——应停止阶段推进，仅保留四要素、排错五项、安全最低集

## 仓库结构

```text
├── README.md          本文件
├── tiangong/
│   ├── SKILL.md       总纲：触发条件、五条总纲、九阶段路由、增补与迭代、跨阶段纪律
│   ├── references/    九阶段细则（进入该阶段时按需阅读）
│   └── templates/     十五份工件骨架（立项书、需求规格、总计划、按次计划、通检表……）
```

## 设计哲学

1. **先约定，后生成**——约定未写明之处，不得各自猜测。
2. **一次一小步**——单次任务只做一个可核对的增量。
3. **形容词不算验收**——判不出过不过的标准不算标准。
4. **一切留痕于仓库**——不依赖对话记录。
5. **人定机做**——越界的决定须向用户提出，不得自行拍板。

## 配套 skill

天工管流程与纪律；下列专用 skill 干具体的活。全部来自开源仓库 [mattpocock/skills](https://github.com/mattpocock/skills)（MIT 许可），可选装——未安装时，天工按自身工序执行同样环节：

| 环节 | skill |
|---|---|
| 立项前拷问需求（给谁用、成功标准、不做什么） | [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) |
| 把已有讨论收束成规格文档 | [to-spec](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec) |
| 把规格/计划拆成带依赖的任务票 | [to-tickets](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) |
| 按规格或任务票实现一块 | [implement](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement) |
| 红—绿—重构做增量（对应阶段六自测） | [tdd](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd) |
| 审查改动（对应合并纪律） | [code-review](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review) |
| 统一术语与领域模型（阶段二/三） | [domain-modeling](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling) |
| 设计与加深模块接口（阶段二） | [codebase-design](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design) |
| 压缩会话为交接文档，另起会话继续 | [handoff](https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff) |
| 对外部问题做高信源调研并落档 | [research](https://github.com/mattpocock/skills/tree/main/skills/engineering/research) |

## 参考与致谢

天工的九阶段流程与纪律为原创（源自作者的「AI 开发实践」课程设计）。部分概念借鉴自下列开源项目——它们均为 **MIT 许可证**；天工只借鉴其**思路**，全部文字与模板为独立撰写，未复制任何代码或文本，无许可合规问题：

- [github/spec-kit](https://github.com/github/spec-kit)——"项目宪法"（constitution）：项目级持久规则文件的思路 → 天工的 `docs/CONSTITUTION.md`
- [obra/superpowers](https://github.com/obra/superpowers)——系统化排错与检查点提交的纪律 → 天工的"根因四步""检查点提交"
- [mattpocock/skills](https://github.com/mattpocock/skills)——"总流程 + 专用 skill 分工"的组合方式 → 天工的调度衔接表（见上）
- [Conventional Commits](https://www.conventionalcommits.org)——提交说明格式的社区约定（仅采用其格式约定）

## 许可证

本仓库以 [MIT 许可证](LICENSE) 开源，可自由使用、修改与分发，仅需保留版权与许可声明。
