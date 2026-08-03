---
name: using-superpowers
description: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions
---

<style>
/* Custom CSS to show the advantages of HTML version */

/* 1. Hide the raw dot graph code block */
pre:has(code.language-dot) {
    display: none !important;
}

/* 2. Style the Red Flags Table */
.superpowers-container table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0 12px;
    margin: 1.5rem 0;
}
.superpowers-container thead {
    display: none; /* Hide header for card-like feel */
}
.superpowers-container tr {
    background: rgba(239, 68, 68, 0.05);
    border: 1px solid rgba(239, 68, 68, 0.15);
    border-radius: 8px;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
    padding: 15px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.15);
}
.superpowers-container tr:hover {
    background: rgba(239, 68, 68, 0.08);
    border-color: rgba(239, 68, 68, 0.35);
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(239, 68, 68, 0.15);
}
.superpowers-container td {
    padding: 6px 0;
    border: none !important;
}
.superpowers-container td:first-child {
    color: #f87171;
    font-weight: bold;
    font-size: 1.05rem;
    position: relative;
    padding-left: 25px;
}
.superpowers-container td:first-child::before {
    content: "🚩";
    position: absolute;
    left: 0;
    top: 5px;
}
.superpowers-container td:last-child {
    color: #34d399;
    font-size: 0.95rem;
    padding-left: 25px;
    position: relative;
}
.superpowers-container td:last-child::before {
    content: "💡";
    position: absolute;
    left: 0;
    top: 5px;
}

/* 3. Style the Interactive Platform Tabs */
.tool-tabs-container {
    margin: 2rem 0;
    background: rgba(25, 18, 50, 0.3);
    border: 1px solid var(--card-border);
    border-radius: 12px;
    padding: 1.5rem;
}
.tab-inputs {
    display: none;
}
.tab-labels {
    display: flex;
    gap: 10px;
    border-bottom: 1px solid var(--card-border);
    padding-bottom: 10px;
    margin-bottom: 15px;
    flex-wrap: wrap;
}
.tab-label {
    padding: 8px 16px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid var(--card-border);
    border-radius: 20px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.9rem;
    transition: all 0.3s ease;
    color: var(--text-muted);
}
.tab-label:hover {
    background: rgba(255, 255, 255, 0.1);
    color: var(--accent);
}
.tab-content {
    display: none;
    animation: fadeIn 0.3s ease;
}
#tab1:checked ~ .tab-labels label[for="tab1"],
#tab2:checked ~ .tab-labels label[for="tab2"],
#tab3:checked ~ .tab-labels label[for="tab3"],
#tab4:checked ~ .tab-labels label[for="tab4"] {
    background: var(--btn-bg);
    color: #fff;
    border-color: transparent;
    box-shadow: 0 0 15px var(--btn-shadow);
}
#tab1:checked ~ .tab-contents #content1,
#tab2:checked ~ .tab-contents #content2,
#tab3:checked ~ .tab-contents #content3,
#tab4:checked ~ .tab-contents #content4 {
    display: block;
}
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(5px); }
    to { opacity: 1; transform: translateY(0); }
}

/* 4. Styled Flow Diagram (Pipeline) */
.flow-pipeline {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin: 2rem 0;
}
.flow-step-card {
    display: flex;
    align-items: center;
    background: rgba(25, 18, 50, 0.25);
    border: 1px solid var(--card-border);
    border-radius: 10px;
    padding: 15px;
    gap: 15px;
    position: relative;
    transition: all 0.3s ease;
}
.flow-step-card:hover {
    border-color: var(--card-hover-border);
    transform: translateX(5px);
}
.flow-step-num {
    width: 35px;
    height: 35px;
    background: var(--btn-bg);
    color: #fff;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    flex-shrink: 0;
    box-shadow: 0 0 10px var(--btn-shadow);
}
.flow-step-desc {
    flex-grow: 1;
}
.flow-step-desc strong {
    display: block;
    color: var(--accent);
    margin-bottom: 2px;
}
.flow-step-desc p {
    margin: 0;
    font-size: 0.9rem;
    color: var(--text-muted);
}

/* 5. Custom Header Card */
.superpowers-header-card {
    background: rgba(139, 92, 246, 0.08);
    border: 1px solid rgba(139, 92, 246, 0.25);
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 25px;
    box-shadow: 0 8px 32px rgba(139, 92, 246, 0.05);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
}
.superpowers-header-card h3 {
    margin-top: 0 !important;
    color: var(--accent);
    font-size: 1.25rem;
    font-weight: 800;
    margin-bottom: 12px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    padding-bottom: 8px;
}
.header-metadata {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    font-size: 0.88rem;
    color: var(--text-muted);
    margin-bottom: 15px;
}
.header-metadata span {
    display: inline-flex;
    align-items: center;
}
.header-links {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 15px;
}
.header-links a {
    color: var(--sidebar-blue) !important;
    text-decoration: none;
    font-weight: 600;
    font-size: 0.92rem;
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
}
.header-links a:hover {
    color: var(--accent) !important;
    transform: translateX(3px);
}
.header-explanation {
    background: rgba(255, 255, 255, 0.02);
    border-left: 3px solid var(--accent);
    padding: 10px 15px;
    border-radius: 0 8px 8px 0;
}
.header-explanation p {
    margin: 0 !important;
    font-size: 0.9rem;
    line-height: 1.5;
}
.header-explanation p:first-child {
    font-weight: bold;
    margin-bottom: 4px !important;
    color: var(--text-main);
}

/* Bilingual text styling */
.zh-desc {
    color: #a78bfa;
    font-size: 0.92rem;
    margin-top: 4px;
    margin-bottom: 12px;
    display: block;
    line-height: 1.5;
}
</style>

<div class="superpowers-container">

<div class="superpowers-header-card">
  <h3>📚 Superpowers Skill 官方規範與導覽說明</h3>
  
  <div class="header-metadata">
    <span>⏱️ <strong>官方最新版本更新時間：</strong>2026-06-18 (v6.0.3 Official Latest)</span>
  </div>
  
  <div class="header-links">
    <a href="https://github.com/obra/superpowers" target="_blank">🌐 官方 GitHub 儲存庫</a>
    <a href="https://falo-taiwan.github.io/superpowers/" target="_blank">🔗 FALO 雙軌教材介紹網頁</a>
    <a href="superpowers_skill_official.md" target="_blank">📄 官方原始 Markdown 技能檔 (English 版)</a>
    <a href="superpowers_skill.md" target="_blank">📝 FALO 專案 Markdown 技能檔 (本機英文代碼版)</a>
    <a href="superpowers_skill.html" target="_blank">📖 FALO HTML 雙語互動好讀版 (本頁)</a>
  </div>
  
  <div class="header-explanation">
    <p>💡 重要說明：</p>
    <p>本檔為 AI 寫程式工具（如 Claude Code / Antigravity / Cursor 等）之 <code>using-superpowers</code> 核心技能規則檔。它被用來塑造 AI 的工程紀律，規範其在開始 any 動作前必須進行技能檢查。此處上傳作為教材實例與雙軌對照，讓大家對照學習「官方原始版」、「FALO 本機版」以及「FALO HTML 雙語好讀版」的差異。</p>
  </div>
</div>

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, skip this skill.
</SUBAGENT-STOP>

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. This is not optional. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## Instruction Priority

Superpowers skills override default system prompt behavior, but **user instructions always take precedence**:

1. **User's explicit instructions** (CLAUDE.md, GEMINI.md, AGENTS.md, direct requests) — highest priority
2. **Superpowers skills** — override default system behavior where they conflict
3. **Default system prompt** — lowest priority

If CLAUDE.md, GEMINI.md, or AGENTS.md says "don't use TDD" and a skill says "always use TDD," follow the user's instructions. The user is in control.

## How to Access Skills

**Never read skill files manually with file tools** — always use your platform's skill-loading mechanism so the skill is properly activated.

* **In Claude Code:** Use the `Skill` tool. When you invoke a skill, its content is loaded and presented to you — follow it directly.
* **In Codex:** Skills load natively. Follow the instructions presented when a skill activates.
* **In Copilot CLI:** Use the `skill` tool. Skills are auto-discovered from installed plugins.
* **In Gemini CLI:** Skills activate via the `activate_skill` tool. Gemini loads skill metadata at session start and activates the full content on demand.
* **In other environments:** Check your platform's documentation for how skills are loaded.

## Platform Adaptation

Skills speak in actions ("dispatch a subagent", "create a todo", "read a file") rather than naming any one runtime's tools. For per-platform tool equivalents and instructions-file conventions, see the interactive tabs below:

<div class="tool-tabs-container">
  <input type="radio" id="tab1" name="platform-tabs" class="tab-inputs" checked>
  <input type="radio" id="tab2" name="platform-tabs" class="tab-inputs">
  <input type="radio" id="tab3" name="platform-tabs" class="tab-inputs">
  <input type="radio" id="tab4" name="platform-tabs" class="tab-inputs">
  
  <div class="tab-labels">
    <label for="tab1" class="tab-label">Claude Code</label>
    <label for="tab2" class="tab-label">Gemini CLI</label>
    <label for="tab3" class="tab-label">Copilot CLI</label>
    <label for="tab4" class="tab-label">Antigravity (AGY)</label>
  </div>
  
  <div class="tab-contents">
    <div id="content1" class="tab-content">
      <p><strong>Claude Code 整合方案</strong>：</p>
      <p>使用 <code>Skill</code> 工具載入與調用。請參閱官方詳細說明：<a href="https://github.com/obra/superpowers/blob/main/skills/using-superpowers/references/claude-code-tools.md" target="_blank">claude-code-tools.md</a> 規範。</p>
    </div>
    <div id="content2" class="tab-content">
      <p><strong>Gemini CLI 整合方案</strong>：</p>
      <p>技能對應表會隨 <code>GEMINI.md</code> 自動載入。請參閱官方詳細說明：<a href="https://github.com/obra/superpowers/blob/main/skills/using-superpowers/references/gemini-tools.md" target="_blank">gemini-tools.md</a> 規範。</p>
    </div>
    <div id="content3" class="tab-content">
      <p><strong>Copilot CLI 整合方案</strong>：</p>
      <p>使用 <code>skill</code> 指令來載入。請參閱官方詳細說明：<a href="https://github.com/obra/superpowers/blob/main/skills/using-superpowers/references/copilot-tools.md" target="_blank">copilot-tools.md</a> 規範。</p>
    </div>
    <div id="content4" class="tab-content">
      <p><strong>Antigravity (AGY) 整合方案</strong>：</p>
      <p>原生支援並相容 Markdown-defined skills 載入。請參閱詳細說明：<a href="https://github.com/obra/superpowers/blob/main/skills/using-superpowers/references/antigravity-tools.md" target="_blank">antigravity-tools.md</a> 規範。</p>
    </div>
  </div>
</div>

# Using Skills

## The Rule

**Invoke relevant or requested skills BEFORE any response or action.** Even a 1% chance a skill might apply means that you should invoke the skill to check. If an invoked skill turns out to be wrong for the situation, you don't need to use it.

### 🔄 技能執行流轉圖 (Skill Execution Flow)

下列為 Markdown 原生定義之 Flowchart，在 HTML 中我們將其轉譯為直觀的時間軸管線：

<div class="flow-pipeline">
  <div class="flow-step-card">
    <div class="flow-step-num">1</div>
    <div class="flow-step-desc">
      <strong>User Message Received (新任務/提問)</strong>
      <p>AI 助理接收到使用者傳送的訊息，啟動分析流程。</p>
    </div>
  </div>
  <div class="flow-step-card">
    <div class="flow-step-num">2</div>
    <div class="flow-step-desc">
      <strong>Might any skill apply? (技能匹配檢測)</strong>
      <p>AI 進入流程思維：這件事是否有對應之 Skill？哪怕只有 1% 可能性，也必須先載入檢測！</p>
    </div>
  </div>
  <div class="flow-step-card">
    <div class="flow-step-num">3</div>
    <div class="flow-step-desc">
      <strong>Announce Skill Usage (主動宣告使用技能)</strong>
      <p>AI 主動對使用者宣告："Using [skill] to [purpose]"，表示已進入該技能的 SOP 約束中。</p>
    </div>
  </div>
  <div class="flow-step-card">
    <div class="flow-step-num">4</div>
    <div class="flow-step-desc">
      <strong>Has Checklist? (檢查清單載入)</strong>
      <p>若技能中包含 checklist 任務清單，則自動在 Agent 工作區中為每一項建立 TODO 任務，並逐一嚴格執行與驗證。</p>
    </div>
  </div>
  <div class="flow-step-card">
    <div class="flow-step-num">5</div>
    <div class="flow-step-desc">
      <strong>Respond / Action (最終回應與產出)</strong>
      <p>執行完畢並取得本輪驗證證據後，AI 才對使用者進行回應或合併代碼。</p>
    </div>
  </div>
</div>

```dot
digraph skill_flow {
    "User message received" [shape=doublecircle];
    "About to enter plan mode?" [shape=doublecircle];
    "Already brainstormed?" [shape=diamond];
    "Invoke brainstorming skill" [shape=box];
    "Might any skill apply?" [shape=diamond];
    "Invoke the skill" [shape=box];
    "Announce: 'Using [skill] to [purpose]'" [shape=box];
    "Has checklist?" [shape=diamond];
    "Create a todo per item" [shape=box];
    "Follow skill exactly" [shape=box];
    "Respond (including clarifications)" [shape=doublecircle];

    "About to enter plan mode?" -> "Already brainstormed?";
    "Already brainstormed?" -> "Invoke brainstorming skill" [label="no"];
    "Already brainstormed?" -> "Might any skill apply?" [label="yes"];
    "Invoke brainstorming skill" -> "Might any skill apply?";

    "User message received" -> "Might any skill apply?";
    "Might any skill apply?" -> "Invoke the skill" [label="yes, even 1%"];
    "Might any skill apply?" -> "Respond (including clarifications)" [label="definitely not"];
    "Invoke the skill" -> "Announce: 'Using [skill] to [purpose]'";
    "Announce: 'Using [skill] to [purpose]'" -> "Has checklist?";
    "Has checklist?" -> "Create a todo per item" [label="yes"];
    "Has checklist?" -> "Follow skill exactly" [label="no"];
    "Create a todo per item" -> "Follow skill exactly";
}
```

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Skill Priority

When multiple skills could apply, use this order:

1. **Process skills first** (brainstorming, systematic-debugging) - these determine HOW to approach the task
2. **Implementation skills second** (frontend-design, mcp-builder) - these guide execution

"Let's build X" → brainstorming first, then implementation skills.
"Fix this bug" → systematic-debugging first, then domain-specific skills.

## Skill Types

**Rigid** (TDD, systematic-debugging): Follow exactly. Don't adapt away discipline.

**Flexible** (patterns): Adapt principles to context.

The skill itself tells you which.

## User Instructions

Instructions say WHAT, not HOW. "Add X" or "Fix Y" doesn't mean skip workflows.

</div>
