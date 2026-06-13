---
name: codebase-narrator
description: Generates developer inner-monologue walkthroughs of codebases — narrating the thought process, decisions, and trade-offs a developer would have while building it, with line-by-line annotations for beginners.
---
# Codebase Narrator

Generate developer-perspective walkthroughs of codebases. The output should read like a developer's internal monologue — not a tutorial, not documentation, but the messy, iterative, "wait-what-if" stream of thought that happens when someone is actually building something.

## When to Activate

Use this skill when the user asks you to:
- Explain how a codebase was built or how a developer would think about it
- Create a walkthrough, narration, or "developer diary" of existing code
- Teach a beginner by showing the thought process, not just the syntax
- Break down a project into the mental steps a developer took

## Output Format

Structure the walkthrough as an **artifact** (markdown document) with these sections:

### 1. The Problem Statement (Act 1)
- Open with the developer asking themselves: "What am I even building?"
- Frame the goal in plain language, no jargon
- List the approaches the developer considered and why they picked the one they did
- Use first-person inner monologue: *"First question I ask myself..."*, *"Two approaches come to mind..."*

### 2. The Architecture (Act 2)
- Explain the high-level structure using ASCII diagrams or tables
- Show how the pieces fit together BEFORE diving into code
- Narrate the developer's reasoning: why these layers, why this separation

### 3. Complete Code Walkthrough (Main Acts)
Walk through EVERY file in the project, in the order a developer would build them. For each file:

- **Open with the developer's thought** in a blockquote: *"Before I write any logic, I need a clean slate."*
- **Show the code in annotated blocks** with inline comments explaining:
  - WHAT the line does (for beginners who may not know the API)
  - WHY it was done this way (the reasoning, trade-offs, alternatives rejected)
  - Common GOTCHAS the developer knows from experience
- **Group related lines** into logical steps (e.g., "STEP 1: Create the gradient", "STEP 2: Draw the wobbly shape")
- **Use tables** to summarize collections of values (constants, parameters, options)

#### Comment Style Rules
- Every comment must start with WHY or WHAT, never just restate the code
- Use conversational tone: *"WHY: We don't want ANY scrollbars..."*
- Include the developer's experiential knowledge: *"I know from past pain that..."*
- Call out non-obvious connections: *"This matches the MASK_COLOR constant so there's no visible seam"*
- For math/algorithms, show concrete examples with actual numbers:
  ```
  t=0.0 -> ease=0.000  (hasn't started growing)
  t=0.2 -> ease=0.488  (already almost half size)
  ```

### 4. Flow Diagram
Include a Mermaid sequence or flow diagram showing the runtime behavior. Rules:
- **NEVER use Mermaid reserved keywords as participant IDs.** Reserved keywords include: `loop`, `alt`, `opt`, `par`, `end`, `rect`, `critical`, `break`, `else`. If a function or concept matches a reserved word (e.g., a function called `loop`), use a different internal ID with a display alias. Example: `participant RenderLoop as loop` instead of `participant Loop as loop`.
- Quote participant names that contain special characters like parentheses
- Avoid parentheses, equals signs, and HTML tags (like `<br/>`) in arrow labels and notes
- Use descriptive labels on arrows
- Add notes for important state changes

### 5. Constants / Config Table
Create a table with every tunable value and the developer's reasoning:

| Constant | Value | Developer's reasoning |
|----------|-------|----------------------|
| NAME     | value | "Why I picked this, in quotes, conversational" |

Emphasize that these values were tuned by feel, not calculated mathematically (when that's the case).

### 6. Concepts Cheat Sheet (for beginners)
A summary table of every technical concept used in the project:

| Concept | What it means | Where it's used |
|---------|---------------|-----------------|

### 7. TL;DR
One-sentence summary of the entire project's trick/mechanism, formatted as a blockquote.

## Voice and Tone Rules

1. **First person, present tense**: Write as if the developer is building it RIGHT NOW. *"Alright, so I need..."*, *"The fix is..."*
2. **No textbook language**: Never say "In this section we will learn..." or "The following code demonstrates...". Say *"This is the artistic core"* or *"This is where all the magic happens."*
3. **Show the mess**: Include the rejected ideas, the trade-offs, the "this felt right" tuning. Real development isn't clean.
4. **Blockquote developer thoughts** before each file section: use `>` quotes for the developer's internal motivation for what they're about to build.
5. **Use "Acts" not "Sections"**: Structure the walkthrough like a story with acts, not a textbook with chapters.
6. **No emojis in code comments**: Keep inline code comments clean and professional. Emojis are fine in section headers.
7. **Link to actual files**: Use clickable file links `[filename](file:///path/to/file)` when referencing project files.
8. **Tables over paragraphs**: When explaining collections of things (constants, concepts, parameters), always prefer tables over prose.

## Quality Checklist

Before finalizing the walkthrough, verify:
- [ ] Every file in the project is covered
- [ ] Every non-trivial line has a WHY comment, not just a WHAT comment
- [ ] The developer's decision-making process is visible (alternatives considered, trade-offs made)
- [ ] Beginners can follow without prior knowledge of the specific APIs used
- [ ] Mermaid diagrams render correctly (participant names with special chars are quoted)
- [ ] Constants are explained with the developer's experiential reasoning, not just definitions
- [ ] The tone reads like a person thinking out loud, not a manual
