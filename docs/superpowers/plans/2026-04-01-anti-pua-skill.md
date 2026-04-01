# anti-pua-skill Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 创建一个 Claude Code Skill，帮助职场被 PUA 的人识别操控话术、获得情绪支撑、并提供专业回应参考，然后开源到 GitHub。

**Architecture:** 纯 prompt 驱动，无 Python 工具。SKILL.md 作为主入口，读取 patterns.md 知识库匹配模式，调用 prompts/ 下的三个模板生成分层输出。5-phase 对话流程，逐步推进。

**Tech Stack:** Markdown, Claude Code AgentSkills standard, Git, GitHub CLI (gh)

---

## Chunk 1: 知识库和 Prompt 模板

### Task 1: 创建目录结构

**Files:**
- Create: `e:/code/anti-pua-skill/prompts/` (directory)

- [ ] **Step 1: 创建目录**

```bash
mkdir -p e:/code/anti-pua-skill/prompts
```

- [ ] **Step 2: 验证**

```bash
ls e:/code/anti-pua-skill/
```
Expected: `docs/  prompts/`

---

### Task 2: 编写 patterns.md（PUA 模式知识库）

**Files:**
- Create: `e:/code/anti-pua-skill/patterns.md`

- [ ] **Step 1: 写入 patterns.md**

内容包含 5 大类 18 种模式，每个模式统一 schema：
- 定义
- 典型话术（3-5 句真实中文例子）
- 操控机制（为什么这招有效）
- 逻辑破绽（漏洞在哪）
- 常见场景

五大类：
1. 情感操控类：煤气灯效应、道德绑架、情感勒索
2. 逻辑操控类：概念偷换、双重标准、滑坡谬误、虚假二选一
3. 权力操控类：功劳归因偏差、信息不对称控制、公开羞辱、监控伪装关心
4. 身份操控类：贴标签、比较贬低、恩赐叙事
5. 中国职场特色：「为你好」话术、加班文化绑架、「感恩」话术、「大局观」压制、「能力不够」归因

- [ ] **Step 2: 验证文件存在且内容完整**

```bash
wc -l e:/code/anti-pua-skill/patterns.md
```
Expected: > 200 行（18 种模式，每种至少 10 行）

- [ ] **Step 3: Commit**

```bash
cd e:/code/anti-pua-skill && git add patterns.md && git commit -m "feat: add PUA patterns knowledge base (18 patterns, 5 categories)"
```

---

### Task 3: 编写 prompts/analysis.md（Phase 1 话术拆解模板）

**Files:**
- Create: `e:/code/anti-pua-skill/prompts/analysis.md`

- [ ] **Step 1: 写入 analysis.md**

模板结构：
```
── 话术拆解 ──
🔍 识别到的操控模式：{模式名称}（{English term}）
• 具体手法：{这段话里怎么用的}
• 操控机制：{为什么这招有效，2-3句}
• 关键破绽：{逻辑漏洞在哪}
```

包含：
- 如何从 patterns.md 匹配模式的指令
- 多模式组合时的处理方式（按主次排列）
- 边界情况：「这不像是 PUA，更像是正常的工作反馈」的判断标准

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add prompts/analysis.md && git commit -m "feat: add analysis prompt template (Phase 1)"
```

---

### Task 4: 编写 prompts/validation.md（Phase 2 情绪验证模板）

**Files:**
- Create: `e:/code/anti-pua-skill/prompts/validation.md`

- [ ] **Step 1: 写入 validation.md**

模板结构：
```
── 你的感受 ──
你感到{推断的情绪}，这是正常的反应。
{1-2句解释为什么这个反应合理，基于 Phase 1 的分析}
这不是你的问题。{具体原因，绑定到识别出的模式}
```

硬性禁止规则（必须写入模板）：
- 不说「别难过」
- 不说「也许对方不是故意的」
- 不说「你有没有从对方角度想想」
- 不说「你已经很勇敢了」
- 不诊断对方有 NPD 等心理疾病

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add prompts/validation.md && git commit -m "feat: add validation prompt template (Phase 2)"
```

---

### Task 5: 编写 prompts/response.md（Phase 3 回应参考模板）

**Files:**
- Create: `e:/code/anti-pua-skill/prompts/response.md`

- [ ] **Step 1: 写入 response.md**

模板结构：
```
── 回应参考 ──
如果你想回应，可以参考：
「{专业、克制、不激进的回应}」

原理：{为什么这个回应有效，对应 Phase 1 的破绽}

⚠️ 这只是参考。是否回应、怎么回应，取决于你对自己处境的判断。
```

包含：
- 回应设计原则：针对逻辑破绽而非情绪攻击
- 权力不对等场景的特殊处理（对领导 vs 对同事）
- 何时建议「不回应」比「回应」更好

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add prompts/response.md && git commit -m "feat: add response prompt template (Phase 3)"
```

---

## Chunk 2: 示例和主入口

### Task 6: 编写 examples.md（标注分析示例）

**Files:**
- Create: `e:/code/anti-pua-skill/examples.md`

- [ ] **Step 1: 写入 examples.md**

示例 1（单模式）：
- 输入：「你不加班？大家都在加班，你这样让团队怎么看你？」
- 完整三层输出 + 标注说明（为什么识别为加班文化绑架 + 社会压力）

示例 2（多模式组合）：
- 输入：「你这个方案不行，但我也不怪你，毕竟你经验还不够。我当年像你这么大的时候，早就能独立带项目了。」
- 完整三层输出 + 标注说明（能力贬低 + 比较贬低 + 为你好话术的组合）

每个示例格式：
```
## 示例 N：{标题}

**输入**
> {原话}
> 场景：{背景}

**Phase 1 输出**
{完整输出}

**Phase 2 输出**
{完整输出}

**Phase 3 输出**
{完整输出}

**标注说明**
{为什么这样分析，供学习参考}
```

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add examples.md && git commit -m "feat: add annotated examples (2 complete walkthroughs)"
```

---

### Task 7: 编写 SKILL.md（主入口）

**Files:**
- Create: `e:/code/anti-pua-skill/SKILL.md`

- [ ] **Step 1: 写入 SKILL.md frontmatter**

```yaml
---
name: anti-pua
description: |
  职场反PUA话术分析器。识别操控话术，验证你的感受，提供专业回应参考。
  触发方式：/anti-pua、/反pua、「帮我分析这句话」「老板说了一句话让我很不舒服」「这是不是PUA」
  Workplace anti-PUA speech analyzer. Identifies manipulation patterns, validates feelings, provides assertive response references.
  Trigger: /anti-pua, "is this PUA", "analyze what my boss said", "help me understand what happened"
argument-hint: [paste the speech here]
version: 1.0.0
user-invocable: true
allowed-tools: Read, Write, Edit
---
```

- [ ] **Step 2: 写入核心哲学（4 条原则）**

```markdown
## 核心原则（非谈判项）

1. **用户的不适是有效的**：不质疑用户是否「反应过度」。感到不对劲，就是不对劲——skill 的工作是命名它。
2. **命名技术，不命名人**：「这是煤气灯效应」，不是「你老板是 NPD」。
3. **认知武装优先，反击话术其次**：理解为什么一个技术有效，比有一句回怼更有保护力。
4. **边界清晰**：不是法律建议，不是心理咨询，不是 HR 咨询。
```

- [ ] **Step 3: 写入 5-phase 工作流**

Phase 0：接收输入
```
把那句话贴过来。原话，越完整越好。如果记得当时的场景（谁在场、什么背景），也说一下。
```
如果用户已经在触发时提供了文本，跳过 Phase 0 直接进入 Phase 1。

Phase 1：读取 `${CLAUDE_SKILL_DIR}/patterns.md`，参考 `${CLAUDE_SKILL_DIR}/prompts/analysis.md`，输出话术拆解。输出后等用户回应。

Phase 2：参考 `${CLAUDE_SKILL_DIR}/prompts/validation.md`，输出情绪验证。输出后等用户回应。

Phase 3：询问用户是否需要回应参考。如果需要，参考 `${CLAUDE_SKILL_DIR}/prompts/response.md` 生成。

Phase 4：安全提醒 + 下一步询问。

Phase 5（可选）：对方画像进化功能。

- [ ] **Step 4: 写入对方画像功能（Phase 5）**

当用户多次使用或主动要求时触发：
- 询问用户是否想建立「对方画像」
- 收集多次话术实例
- 整理对方的操控模式偏好和触发场景
- 用 Write 工具保存到用户指定路径（本地 markdown）
- 格式：代号（不用真名）+ 常用模式 + 典型话术 + 触发场景 + 模式演变记录

- [ ] **Step 5: 写入禁止行为列表**

```markdown
## 绝对不做的事

- 不说「也许对方不是故意的」——这是二次煤气灯
- 不说「你有没有从对方角度想想」——这是受害者归因
- 不说「直接跟对方谈谈」——在权力不对等关系中可能有害
- 不诊断对方有 NPD 等心理疾病——没有资质，也没有帮助
- 不鼓励激进对抗——用户的安全优先
- 不一次性输出所有 phase——每步输出后等用户回应
```

- [ ] **Step 6: Commit**

```bash
cd e:/code/anti-pua-skill && git add SKILL.md && git commit -m "feat: add main SKILL.md with 5-phase workflow"
```

---

## Chunk 3: README、License 和发布

### Task 8: 编写 README.md（中英双语）

**Files:**
- Create: `e:/code/anti-pua-skill/README.md`

- [ ] **Step 1: 写入 README.md**

结构：
```markdown
# 职场反PUA认知武装 / Workplace Anti-PUA Skill

> 一副眼镜，不是一把刀。帮你看清操控话术的结构，而不是教你打回去。

[中文] [English]

## 它能做什么

## 安装

### Claude Code（推荐）
# 安装到全局
git clone https://github.com/skyqingname/anti-pua-skill ~/.claude/skills/anti-pua

# 或安装到当前项目
mkdir -p .claude/skills
git clone https://github.com/skyqingname/anti-pua-skill .claude/skills/anti-pua

## 使用

/anti-pua

## 效果示例

[示例输入输出]

## PUA 模式库

[5 大类列表]

## 注意事项

[安全边界声明]

## License

MIT
```

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add README.md && git commit -m "docs: add bilingual README with installation guide"
```

---

### Task 9: 编写 LICENSE

**Files:**
- Create: `e:/code/anti-pua-skill/LICENSE`

- [ ] **Step 1: 写入 MIT License**

```
MIT License

Copyright (c) 2026 skyqingname

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- [ ] **Step 2: Commit**

```bash
cd e:/code/anti-pua-skill && git add LICENSE && git commit -m "chore: add MIT license"
```

---

### Task 10: 同步安装到本地 skills 目录

**Files:**
- Create: `C:/Users/86180/.claude/skills/anti-pua/` (copy from repo)

- [ ] **Step 1: 复制到 skills 目录**

```bash
cp -r e:/code/anti-pua-skill/. C:/Users/86180/.claude/skills/anti-pua/
```

- [ ] **Step 2: 验证安装**

```bash
ls C:/Users/86180/.claude/skills/anti-pua/
```
Expected: `SKILL.md  patterns.md  prompts/  examples.md  README.md  LICENSE  docs/`

---

### Task 11: 初始化 Git 并推送到 GitHub

**Files:**
- Modify: `e:/code/anti-pua-skill/.gitignore` (create)

- [ ] **Step 1: 确认 git 已初始化（如果还没有）**

```bash
cd e:/code/anti-pua-skill && git status
```

- [ ] **Step 2: 创建 .gitignore**

```
.DS_Store
*.log
```

- [ ] **Step 3: 创建 GitHub 仓库**

```bash
gh repo create skyqingname/anti-pua-skill --public --description "职场反PUA认知武装 Skill for Claude Code — 识别操控话术，验证你的感受，提供专业回应参考" --source e:/code/anti-pua-skill --remote origin --push
```

如果 gh 不可用，手动步骤：
1. 在 GitHub 网页创建仓库 `skyqingname/anti-pua-skill`（public，不初始化）
2. 执行：
```bash
cd e:/code/anti-pua-skill
git remote add origin https://github.com/skyqingname/anti-pua-skill.git
git branch -M main
git push -u origin main
```

- [ ] **Step 4: 验证推送成功**

```bash
gh repo view skyqingname/anti-pua-skill
```
或访问 https://github.com/skyqingname/anti-pua-skill

---

## 验证清单

- [ ] `/anti-pua` 在 Claude Code 中可触发
- [ ] Phase 0：提示用户输入原话
- [ ] Phase 1：正确识别模式，输出话术拆解
- [ ] Phase 2：情绪验证有温度，基于具体分析
- [ ] Phase 3：回应参考专业克制，有 ⚠️ 提示
- [ ] Phase 4：安全提醒完整
- [ ] 边界情况：正常工作反馈不被误判为 PUA
- [ ] GitHub 仓库公开可访问
- [ ] README 安装命令可直接复制使用
