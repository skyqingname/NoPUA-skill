# 反PUA斗士

> 当你看清问题的时候问题就已解决了大半，对PUA勇敢say nooooo！
> Identifying the problem is half the solution. Have the courage to say nooooo to PUA!

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

[中文](#中文) · [English](#english)

---

## 中文

### 它能做什么

三层输出：
1. **话术拆解**（认知武装）：识别操控模式，命名手法，找出逻辑破绽
2. **情绪验证**（情绪出口）：验证你的感受是合理的，说清楚为什么这不是你的问题
3. **回应参考**（可选）：提供一个专业、克制的回应，附带原理说明

### 安装

#### Claude Code（推荐）

```bash
# 安装到全局（所有项目都能用）
git clone https://github.com/skyqingname/anti-pua-skill ~/.claude/skills/anti-pua

# 或安装到当前项目
mkdir -p .claude/skills
git clone https://github.com/skyqingname/anti-pua-skill .claude/skills/anti-pua
```

### 使用

```
/anti-pua
```

或直接贴入话术：

```
/anti-pua 你这个方案不行，但我也不怪你，毕竟你经验还不够。
```

### 效果示例

输入：`「你不加班？大家都在加班，你这样让团队怎么看你？」`

```
── 话术拆解 ──
🔍 识别到的操控模式：加班文化绑架（Overtime Culture Coercion）
• 具体手法：用"大家都在加班"制造群体压力，将个人的正常下班行为框定为对团队的背叛。
• 操控机制：不直接命令加班，而是通过暗示"所有人都在做"来制造从众压力。
• 关键破绽：工作成果的衡量标准应该是产出质量，不是在工位上的时长。

🔍 识别到的操控模式：公开羞辱（Public Shaming）
• 具体手法：选择当着同事的面质问，而非私下沟通，将个人工作安排变成公开审判。
• 操控机制：公开场合的质问同时攻击了尊严和社会形象，旁观者也会因此更不敢准时下班。
• 关键破绽：如果目的是讨论工作安排，私下沟通效率更高。选择当众说，说明目的是制造社交压力。
```

### PUA 模式库（18 种，5 大类）

**情感操控类**：煤气灯效应、道德绑架、情感勒索

**逻辑操控类**：概念偷换、双重标准、滑坡谬误、虚假二选一

**权力操控类**：功劳归因偏差、信息不对称控制、公开羞辱、监控伪装关心

**身份操控类**：贴标签、比较贬低、恩赐叙事

**中国职场特色**：「为你好」话术、加班文化绑架、「感恩」话术、「大局观」压制

### 注意事项

- 这是认知支持工具，不是法律建议或心理咨询
- 如果你正在经历持续的职场霸凌，建议保留证据并咨询专业律师
- 本工具不鼓励激进对抗，用户的安全优先

---

## English

### What it does

Three-layer output:
1. **Speech Analysis** (Cognitive Armor): Identifies manipulation patterns, names the technique, exposes the logical flaw
2. **Emotional Validation**: Validates your feelings with specific reasoning — not generic comfort
3. **Response Reference** (Optional): A professional, measured response with explanation of why it works

### Installation

#### Claude Code (Recommended)

```bash
# Install globally (available in all projects)
git clone https://github.com/skyqingname/anti-pua-skill ~/.claude/skills/anti-pua

# Or install in current project
mkdir -p .claude/skills
git clone https://github.com/skyqingname/anti-pua-skill .claude/skills/anti-pua
```

### Usage

```
/anti-pua
```

Or paste the speech directly:

```
/anti-pua Your proposal doesn't work, but I don't blame you — you just don't have enough experience yet.
```

### Pattern Library (18 patterns, 5 categories)

**Emotional Manipulation**: Gaslighting, Moral Blackmail, Emotional Blackmail (FOG)

**Logic Manipulation**: Concept Substitution, Double Standards, Slippery Slope, False Dilemma

**Power Manipulation**: Credit Manipulation, Information Asymmetry, Public Shaming, Surveillance as Care

**Identity Manipulation**: Labeling, Comparative Devaluation, Benefactor Narrative

**Chinese Workplace Specific**: Paternalistic Manipulation ("For Your Own Good"), Overtime Culture Coercion, Gratitude Manipulation, Big Picture Suppression

### Important Notes

- This is a cognitive support tool, not legal advice or psychological counseling
- If you are experiencing ongoing workplace bullying, document evidence and consult a qualified attorney
- This tool does not encourage aggressive confrontation — your safety comes first

---

## License

MIT © skyqingname
