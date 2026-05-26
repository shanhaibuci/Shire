# Shire Quiz Repository

本仓库已按 `skills/quiz-repo-spec` 重构为可同步的 `md-quiz` 仓库。

## 结构

```text
.
├── md-quiz-repo.yaml
├── quizzes/
│   ├── common-test-2025/
│   │   ├── quiz.md
│   │   └── assets/
│   ├── ai-workstyle-50/
│   │   └── quiz.md
│   ├── ai-rd-engineer-screening-50/
│   │   └── quiz.md
│   ├── personality-type-5d-80/
│   │   └── quiz.md
│   ├── parser-smoke-5/
│   │   ├── quiz.md
│   │   └── assets/
│   └── tech-media-ops-intern-screening/
│       └── quiz.md
├── job-descriptions/
│   ├── algorithm-intern/
│   │   └── jd.md
└── skills/
```

## Quiz 列表

- `common-test-2025`: 共性能力测试2025
- `ai-workstyle-50`: AI 时代工作方式问卷（50题）
- `ai-rd-engineer-screening-50`: AI 研发工程师招聘初筛问卷（50题）
- `personality-type-5d-80`: 人格类型测试（五维版·80题）
- `parser-smoke-5`: 系统解析测试问卷（5题）
- `tech-media-ops-intern-screening`: 技术类自媒体运营实习生招聘初筛问卷

每份 `quiz.md` 的 Front Matter 现支持 `tags`，用于分类、检索和后续筛选。
其中 `common-test-2025`、`tech-media-ops-intern-screening` 与 `ai-rd-engineer-screening-50` 属于招聘/筛选型混合问卷。
`ai-rd-engineer-screening-50` 属于研发工程习惯 / AI 工程筛选方向的高难度混合问卷。
`parser-smoke-5` 用于验证 welcome/end image、media、traits、`[rubric]`、`[llm]` 等解析要素。

## 职位列表

- `algorithm-intern`: 算法实习生
  - 关联问卷：`ai-rd-engineer-screening-50`、`common-test-2025`

职位文件位于 `job-descriptions/<jd_key>/jd.md`，使用 YAML Front Matter 维护 `id`、`title`、`status`、`tags` 与 `related_quizzes`。正文保存岗位职责、任职要求和筛选侧重点。

## Skills

仓库内当前维护一个推荐安装的总入口 skill，以及两份底层 skill：

- [`md-quiz`](./skills/md-quiz/SKILL.md)
  推荐作为默认安装入口。用于“我要维护 md-quiz 问卷”这类泛化任务，负责把问题分流到 QML 语法层或仓库结构层。

- [`qml-authoring`](./skills/qml-authoring/SKILL.md)
  用于编写、修订和校验 `quiz.md` 的 QML 语法，包括题头格式、`answer_time`、`[rubric]`、首尾图片和 parser 边界。对应参考规范见 [`qml-spec.md`](./skills/qml-authoring/references/qml-spec.md)。
- [`quiz-repo-spec`](./skills/quiz-repo-spec/SKILL.md)
  用于维护可同步的问卷仓库结构，包括 `md-quiz-repo.yaml`、`quizzes/<quiz_id>/quiz.md`、`assets/` 路径和同步契约。对应参考规范见 [`repo-contract.md`](./skills/quiz-repo-spec/references/repo-contract.md)。

## 协作约定

面向协作者和自动化代理的仓库操作约定见 [`AGENTS.md`](./AGENTS.md)。

## 问卷路线图

后续问卷建设建议优先考虑三类形态：

- 知识题 / 能力题：适合 `single`、`multiple`、`short`
- 量表题 / 倾向题：适合 `single + {scoring=traits}`
- 混合问卷：同时包含知识题与倾向题

### 优先级建议

其中 `ai-workstyle-50` 已经落地；后续优先建设以下 4 类问卷：

1. 团队协作风格问卷
2. 职业兴趣问卷
3. 领导力与执行力倾向问卷
4. 学习风格与成长路径问卷

原因：

- 能与现有两份问卷形成组合包
- 都适合用 `single + traits` 建模
- 面向招聘、培训、组织发展都有直接用途

### 第一梯队

- 团队协作风格问卷
  目标：识别沟通方式、协作偏好、冲突处理方式、责任边界。
  推荐题量：40-60 题。
  推荐 tags：`[teamwork, collaboration, communication, conflict, self-assessment]`
  推荐形式：`single + {scoring=traits}`

- 职业兴趣问卷
  目标：判断更偏产品、研发、运营、销售、研究、设计等方向。
  推荐题量：50-80 题。
  推荐 tags：`[career, interest, role-fit, self-assessment, orientation]`
  推荐形式：`single + {scoring=traits}`

- 领导力与执行力倾向问卷
  目标：评估授权、目标感、推动力、反馈方式、压力承担。
  推荐题量：40-60 题。
  推荐 tags：`[leadership, execution, management, responsibility, self-assessment]`
  推荐形式：`single + {scoring=traits}`

### 第二梯队

- 学习风格与成长路径问卷
  推荐 tags：`[learning, growth, study-style, training, self-assessment]`
  推荐形式：`single + {scoring=traits}`

- 产品经理能力画像问卷
  推荐 tags：`[product, pm, prioritization, user-insight, role-fit]`
  推荐形式：混合问卷

- 研发工程习惯问卷
  推荐 tags：`[engineering, coding, quality, testing, developer]`
  推荐形式：混合问卷

- 数据分析思维问卷
  推荐 tags：`[data, analysis, metrics, experimentation, reasoning]`
  推荐形式：混合问卷

- AI 研发工程师招聘初筛问卷
  推荐 tags：`[recruitment, screening, ai, llm, engineering, rag, agent, evaluation]`
  推荐形式：混合问卷

### 第三梯队

- 职业价值观问卷：`[values, career, motivation, self-assessment]`
- 决策风格问卷：`[decision-making, thinking-style, self-assessment]`
- 压力应对与韧性问卷：`[resilience, stress, coping, self-assessment]`
- 远程办公协作习惯问卷：`[remote-work, collaboration, communication, workflow]`

### 谨慎建设的方向

以下题目不建议在当前仓库中直接作为普通问卷推出：

- 抑郁、焦虑、人格障碍、ADHD 等临床或准临床心理测评
- 医疗诊断、法律风险、投资适当性等高风险判断型问卷

### 建设建议

后续创建新问卷时，优先遵循以下顺序：

1. 先确定用途：筛选、画像、培训还是自我认知
2. 再确定建模：知识题、量表题还是混合题
3. 为问卷补齐 Front Matter：`id`、`title`、`description`、`tags`、`question_count`、`question_counts`、`estimated_duration_minutes`
4. 若是倾向类问卷，优先用 `single + {scoring=traits}`
5. 若是能力类问卷，优先用 `single` / `short`
