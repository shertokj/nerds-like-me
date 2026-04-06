# 🦞 Nerds Like Me — Agent Skill Hackathon: Participant Guide

**Pop-up Hackathon: AI Agent Skills**
**Tuesday, April 7th, 2026 · 7:15 PM – 9:30 PM CDT**
**Highwood, IL**

---

## Table of Contents

1. [Welcome](#1-welcome)
2. [What Is an AI Agent Skill?](#2-what-is-an-ai-agent-skill)
3. [Record-Transcribe-Refine: The Beginner Workflow](#3-record-transcribe-refine-the-beginner-workflow)
4. [SKILL.md Anatomy](#4-skillmd-anatomy)
5. [Setting Up OpenClaw](#5-setting-up-openclaw)
6. [Project Ideas by Tier](#6-project-ideas-by-tier)
7. [The 5 Skill Killers](#7-the-5-skill-killers)
8. [When Things Go Wrong — Troubleshooting](#8-when-things-go-wrong--troubleshooting)
9. [What Skills Can't Do](#9-what-skills-cant-do)
10. [Advanced Topics](#10-advanced-topics)
11. [Real-World Inspiration](#11-real-world-inspiration)
12. [Resources](#12-resources)
13. [Share Your Skill](#13-share-your-skill)
14. [Cheat Sheet](#14-cheat-sheet)

---

## 1. Welcome

### What Is This Event?

A **pop-up hackathon** where you'll build a real, working AI agent skill in 2.5 hours. Not a lecture. Not a workshop where you watch someone else code. You'll walk in knowing nothing about agent skills and walk out with one that works.

The theme: **"Teach AI to do the work you already do."**

You already have workflows. Meeting notes, follow-up emails, status updates, deal memos, reports. Today you'll teach an AI to handle one of them.

Anthropic frames this perfectly: **"Don't build agents, build skills instead."** ([Watch the talk](https://www.youtube.com/watch?v=CEvIs9y1uog)) The idea is simple — rather than trying to build a monolithic autonomous agent that "does everything," you build small, focused skills that do one thing well. That's exactly what we're doing tonight.

### No Experience Needed

- You don't need to know how to code.
- You don't need to have used an AI agent before.
- You need a laptop, a browser, and a task you do repeatedly.
- You'll leave with a working skill. We promise.

### The NLM Vibe

🦞 **Nerds Like Me** is a community of curious people who like to build, break, and figure things out together. This hackathon follows the same rules: be generous with what you know, ask the "dumb" questions, and help your tablemates.

---

## 2. What Is an AI Agent Skill?

### The Chef & Recipe Analogy

Imagine a chef who's talented but has no recipes. You ask for a specific dish — they'll figure it out, but the result depends on their mood, their interpretation, and a lot of guesswork.

Now give that chef a detailed recipe. Same skills, but now they execute precisely, consistently, and they can handle edge cases the recipe anticipated.

- A **general-purpose AI agent** (Claude, GPT, Gemini, etc.) is the **Chef** — it knows how to cook.
- An **Agent Skill** is the **Recipe** — a reusable set of instructions that tells the chef exactly how to prepare a specific dish.

Without skills: the chef guesses. With skills: the chef executes.

### What Exactly Is a Skill?

A skill is **a markdown file that teaches an AI agent how to perform a specific task.**

That's it. No compilers, no deployment pipelines, no SDKs. It's structured instructions in a text file, optionally accompanied by scripts, reference documents, and templates.

Here's how it works:

1. You create a folder with a `SKILL.md` file inside it.
2. The agent reads the description field in that file to understand when to use it.
3. When a relevant request comes in, the agent loads the skill and follows the instructions.
4. The skill produces output — an email, a report, formatted notes, whatever you designed it to do.

Claude's own one-minute overview of Agent Skills is a great primer: [Watch here](https://www.youtube.com/watch?v=VRzkafNIdgI).

### Key Characteristics

**Skills are primarily structured instructions.** Think of them as "onboarding documents for an AI." You're telling the agent exactly what to do, step by step, in plain English (or whatever language you prefer). As Anthropic puts it in their [Complete Guide to Building Skills](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf): a skill is a modular, reusable package of instructions, scripts, and domain expertise that tells the agent exactly how to execute a specific task.

**Skills can include supporting scripts.** Need a Python script to transform data? A shell script to validate a config? Put them in a `scripts/` directory and the skill can run them.

**Skills are non-deterministic.** This is important: the same skill will produce slightly different output each time you run it. The agent interprets your instructions, and interpretation varies. This is normal and expected. Don't treat skills as guaranteed outputs — treat them as rough drafts that get better with iteration.

**Skills are force-multipliers, not autonomous workers.** A skill doesn't replace your judgment. It handles the repetitive, structured part of a task so you can focus on the parts that actually require a human. You review the output, make adjustments, and send it.

### Capabilities vs. Preferences

One of the most common mistakes: confusing a capability with a preference.

- ✅ **Capability:** "Format my meeting notes into a structured summary with action items, decisions, and attendees." (This is automatable.)
- ❌ **Preference:** "Write in my exact voice with my specific tone and humor." (This is subjective — you'll always need to edit.)

A good skill automates a **capability** — the mechanical, repeatable part of a task. It doesn't try to replicate your unique style (though it can get close with good examples in the instructions).

---

## 3. Record-Transcribe-Refine: The Beginner Workflow

This is **THE method** for beginners. Do not try to "write a skill from scratch." That's how you end up staring at a blank screen.

### Step 1: Record Yourself Doing the Task

How do you actually do the thing you want to automate? Record it.

Options:
- **Screen recording** (macOS: Cmd+Shift+5, Windows: Win+G) — record yourself doing the task in real time
- **Voice memo** — talk through the steps out loud
- **Written steps** — open a notepad and write down exactly what you do, in order

Example: You write a weekly status update every Friday. Record yourself doing it. What do you think about first? What do you include? What do you leave out? How do you format it?

### Step 2: Transcribe Into Structured Instructions

Take your recording or notes and turn it into markdown instructions. Be specific. Include:

- What inputs the skill needs
- What steps to follow (in order)
- What the output should look like
- Any rules or constraints ("don't invent data," "keep it under 200 words")

You don't need to write perfect instructions. Rough is fine. You'll refine in Step 3. If you're stuck, feed your raw notes to an AI and say: *"Turn this into a SKILL.md for OpenClaw."* It'll get you 80% of the way there.

### Step 3: Test with the AI Agent. Refine.

Run your skill. Feed it real input — the same kind of data you'd normally work with. Compare the output to what you'd produce yourself.

Ask yourself:
- Did it miss anything important?
- Is the format right?
- Is there anything extra you didn't want?
- Would you send this output as-is, or do you need to edit it?

Then go back and refine the instructions. Add specificity. Add examples. Add edge case handling. Test again. Repeat until the output matches what you'd produce.

### Worked Example: Weekly Status Update Skill

**Step 1 (Record):** "Every Friday I write a status update. I think about what I accomplished, what I'm doing next week, and if anything is blocked. I keep it short — bullet points. I flag anything urgent. My manager reads it, so I keep it professional."

**Step 2 (Transcribe):**
```markdown
---
name: weekly-status-update
description: Generate a structured weekly status update from rough notes about what you accomplished, what's next, and any blockers. Use every Friday.
---

Take the rough weekly update notes provided and turn them into a structured status update.

## Required Sections
1. **Accomplishments This Week** (bullet points, max 5)
2. **Priorities for Next Week** (bullet points, max 5)
3. **Blockers & Risks** (anything that needs attention or escalation)
4. **Key Metrics / Numbers** (any quantifiable results)

## Rules
- Don't invent accomplishments not in the raw notes
- Keep the total output under 200 words
- Flag anything time-sensitive with ⚠️
```

**Step 3 (Test & Refine):** Feed it your rough notes from this week. Check the output. Add refinements like "Use professional tone, no emojis" or "Always include date at the top" based on what's missing.

### Why This Works

You're not guessing what instructions the AI needs. You're documenting what **actually works** — your own proven process. The AI is just executing your expertise at scale.

### The Iteration Mindset

> "The first version won't be perfect. That's normal. Iterate on instructions until the output matches what you'd produce."

Nobody ships a perfect skill on the first try. Plan for 3-5 rounds of testing and refinement. Each round gets you closer to output that's good enough to use directly.

---

## 4. SKILL.md Anatomy

A skill is a folder containing at minimum a `SKILL.md` file. Here's the full anatomy:

### Folder Structure

```
my-skill/
├── SKILL.md              (required — the recipe)
├── scripts/              (optional — executable code)
│   └── validate.sh
├── references/           (optional — docs loaded on demand)
│   └── api-docs.md
└── assets/               (optional — templates, images)
    └── template.md
```

Most beginner skills are just a single `SKILL.md` file. You only add `scripts/`, `references/`, and `assets/` when your skill needs them.

### YAML Frontmatter

The top of every `SKILL.md` starts with YAML frontmatter between `---` delimiters:

```yaml
---
name: my-skill
description: What this skill does and when to trigger it. This is how the agent discovers the skill.
---
```

| Field | Required? | Purpose |
|-------|-----------|---------|
| `name` | Yes | Identifier for the skill. Use kebab-case (e.g., `weekly-status-update`). |
| `description` | Yes | **This is how the agent discovers your skill.** Write a clear, specific description of what the skill does and when it should be used. The agent matches user requests against this field to decide whether to load your skill. If your description is vague, the skill won't trigger. Be explicit about the use case and the keywords a user might say. |

**The description field is the most important part of your skill.** Write it carefully. It should answer: *What does this skill do? When should it be used? What words would a person naturally say when they need this?*

### Markdown Body

After the frontmatter, write your instructions in markdown:

```markdown
# My Skill Name

A brief explanation of what this skill does and when to use it.

## Input

What the user needs to provide (notes, a file, a URL, etc.).

## Steps

1. **First step** — do this thing
2. **Second step** — then do this thing
3. **Third step** — finally do this thing

## Output Format

Exactly what the output should look like. Give examples.

## Rules & Constraints

- Don't invent data that wasn't provided
- Keep output under X words
- Always include Y
- Never do Z
```

### Complete Annotated Template

```markdown
---
# Required fields
name: client-follow-up-email
description: >
  Formats a professional follow-up email after a client meeting or call.
  Takes rough notes from the conversation and produces a polished email
  with summary points, action items, and next steps. Triggered when the
  user says "follow up," "meeting follow-up," or "send a recap."
---

# Client Follow-Up Email Formatter

This skill turns rough notes from a client meeting or phone call into a
professional follow-up email ready to send.

## Input

The user provides rough notes from a meeting or call. These may be:
- Bullet points
- Voice-to-text dictation
- Typed notes from during the meeting
- Any combination of the above

The user may also optionally provide:
- Client name
- Meeting date
- Any specific topics they want emphasized

## Steps

1. **Read the raw notes carefully.** Identify:
   - Key discussion points
   - Decisions made
   - Action items (who is doing what, by when)
   - Open questions or follow-ups needed
   - Any deadlines mentioned

2. **Draft the email.** Structure it as:
   - **Subject line:** Specific and actionable (e.g., "Follow-up: [Main Topic] — [Client Name]")
   - **Opening:** Thank them for their time, reference the meeting date
   - **Summary:** 2-3 sentences covering what was discussed
   - **Action Items:** Numbered list with owners and deadlines
   - **Next Steps:** What happens next and any timeline
   - **Closing:** Professional sign-off

3. **Review and polish.**
   - Tone: professional but warm (not stiff)
   - Length: 150-250 words total
   - No jargon unless the client uses it
   - If anything is ambiguous in the notes, flag it with [VERIFY] so the user can fill in the gap

## Output Format

```
Subject: [Your subject line here]

Hi [Client Name],

Thanks for the great conversation on [date]. Here's a recap of what we discussed:

[2-3 sentence summary]

**Action Items:**
1. [Action] — [Owner] — [Deadline]
2. [Action] — [Owner] — [Deadline]

**Next Steps:**
[What happens next]

Best,
[User's name]
```

## Rules

- Don't invent discussion points or action items not present in the notes
- If the notes are vague about who owns an action item, assign to [USER]
- Keep the total email under 250 words
- Don't use bullet points in the email body (use numbered lists for action items, prose for everything else)
- Always include a subject line
- If the user provides a specific tone preference, follow it over the defaults above
```

### Key Best Practices for Instructions

1. **Be specific.** "Format the email professionally" is vague. "Tone: professional but warm, 150-250 words, include subject line" is specific.
2. **Give examples.** Show what good output looks like. The agent will mimic the pattern.
3. **Handle edge cases.** What if the notes are really short? What if they're disorganized? What if there are no action items? Tell the agent what to do.
4. **Specify output format.** Use a template. Show exactly what the output should look like.
5. **State constraints clearly.** Word limits, tone rules, things never to do.
6. **Keep it focused.** One skill, one job. If you're trying to solve your whole workflow, split it into multiple skills.

> **A working skill can be as short as 10 lines of markdown.** Don't overcomplicate your first one. Start simple, add complexity as you iterate.

---

## 5. Setting Up OpenClaw

### What You Need

- A computer (macOS or Linux recommended; Windows works with WSL)
- A terminal (macOS: Terminal.app; Windows: PowerShell or WSL)
- An OpenClaw account or Claude Code
- A code editor (VS Code recommended, but any text editor works)

### Option A: OpenClaw Sandbox (Fastest — No Install)

If you want to skip installation entirely:

1. Go to [campclaw.ai](https://campclaw.ai/)
2. Create a free account
3. Start a new session in the browser-based sandbox
4. Create skills directly in the web interface

The sandbox has everything you need to build and test skills without installing anything on your computer.

### Option B: OpenClaw Local Install

For a full local setup:

1. Sign up at [openclaw.ai](https://openclaw.ai)
2. Install OpenClaw following the platform docs at [docs.openclaw.ai](https://docs.openclaw.ai)
3. Configure your API keys (Anthropic, OpenAI, etc.)
4. Start the gateway: `openclaw gateway start`

### Where Do Skills Live?

```
~/.openclaw/workspace/skills/<skill-name>/SKILL.md    (your personal skills)
~/.openclaw/skills/<skill-name>/SKILL.md               (shared/installed skills)
```

Skills are auto-discovered by the agent based on description matching. When you create a skill in the right folder, the agent finds it automatically.

### Install Community Skills

Browse and install skills from the [OpenClaw skills marketplace](https://www.clawhub.ai/skills):

```bash
openclaw skills install <skill-name>    # Install a skill from ClawHub
openclaw skills list                    # See all loaded skills
```

### Option C: Claude Code (Alternative)

Claude Code has partial SKILL.md support via `.claude/commands/`. The format is similar but discovery and features differ from OpenClaw.

- Install Claude Code: `npm install -g @anthropic-ai/claude-code`
- Skills go in `.claude/commands/` in your project directory
- See [Claude Code Customization Guide](https://alexop.dev/posts/claude-code-customization-guide-claudemd-skills-subagents/) for details

### Verify Your Setup

```bash
openclaw skills list          # Should show your installed skills
openclaw skills install hello # Test install from ClawHub
```

If those commands work, you're ready to build.

---

## 6. Project Ideas by Tier

Pick the tier that matches your experience level. If you've never built a skill before, start at **Tier 1** no matter how technical you are in other areas.

---

### Tier 1: Beginner (No Technical Background)

**Goal:** Build your first working skill using Record-Transcribe-Refine. Ship something.

These take 15-20 minutes. Pick the one closest to a task you already do.

#### Client Follow-Up Email Formatter

**What it does:** Takes rough notes from a client meeting or phone call and formats a professional follow-up email with a summary, action items (with owners and deadlines), and next steps.

**Who it's for:** Anyone who has client-facing conversations — consultants, wealth advisors, real estate professionals, insurance brokers, recruiters.

**How to build it:**
1. **Record:** Think about how you write follow-up emails right now. What do you always include? What format do you use?
2. **Transcribe:** Write instructions for what the email should contain (subject line, opening, summary, action items, closing)
3. **Refine:** Test with real meeting notes. Add constraints (word limit, tone rules, what to do with vague notes)
4. **Tip:** Include an output template in the instructions so the agent knows exactly what format to produce

#### Weekly Status Update Generator

**What it does:** Takes rough notes about your week and formats a clean, structured status update with accomplishments, priorities, and blockers.

**Who it's for:** Anyone who writes weekly updates — nurses, product managers, engineers, business owners.

**How to build it:**
1. **Record:** What sections do your status updates always have? What does your manager care about?
2. **Transcribe:** Define the required sections (accomplishments, next week, blockers, metrics)
3. **Refine:** Add rules like "don't invent accomplishments" and "keep under 200 words"
4. **Tip:** Add a ⚠️ flag for time-sensitive items

#### Meeting Notes Formatter

**What it does:** Takes raw meeting notes (typed, dictated, or rough bullet points) and outputs a structured summary with attendees, discussion topics, decisions made, and action items.

**Who it's for:** Anyone who takes meeting notes — period. This is the most universally useful beginner skill.

**How to build it:**
1. **Record:** How do you structure meeting notes now? What do you always capture?
2. **Transcribe:** Define output sections (attendees, topics discussed, decisions, action items with owners/deadlines)
3. **Refine:** Test with a real meeting's notes. Handle edge cases (what if there are no decisions? What if notes are very short?)
4. **Tip:** Add a "Date" and "Meeting Title" field that the agent fills in from context

---

### Tier 2: Intermediate (Some Technical Background)

**Goal:** Build something you'd actually use at work every day.

These take 25-30 minutes. They may use web fetching, file reading, or structured output.

#### GitHub Issue Summarizer

**What it does:** Takes a GitHub issue URL, fetches it, and produces a concise summary with labels, assignee, priority assessment, and suggested next steps.

**What you learn:** Web fetching, API interaction, structured analysis.

**How to build it:**
1. Write instructions for the agent to fetch the issue URL
2. Define the output format: title, summary (2-3 sentences), labels, assignee, priority assessment, recommended action
3. Test with real GitHub issues from your own repos or popular open-source projects

#### Email Drafter

**What it does:** Takes context (recipient, topic, desired tone) and drafts a professional email with a subject line and appropriate formatting.

**What you learn:** Tone control, templates, context-aware generation.

**How to build it:**
1. Define input fields: recipient role, topic, tone (formal/casual/friendly), key points to cover
2. Create output template with subject line, body, and closing
3. Test with real email scenarios you face at work

#### Config File Validator

**What it does:** Reads a JSON or YAML config file and checks for common mistakes: missing required fields, type mismatches, invalid values, deprecated options.

**What you learn:** Schema validation, error reporting, the `references/` directory pattern.

**How to build it:**
1. Create a `references/config-schema.md` file listing the required fields, their types, and valid values
2. Write instructions for the agent to read the config file, compare against the schema, and report issues
3. Test with intentionally broken config files

#### Client Follow-Up Email Formatter (Advanced Version)

**What it does:** Same as the Tier 1 version, but with:
- A `references/voice-guide.md` for your specific email style
- Multiple templates (initial meeting, check-in, proposal follow-up, project wrap-up)
- CRM-ready output format

**What you learn:** Progressive disclosure with `references/`, template selection, output adaptation.

---

### Tier 3: Take-Home Challenges

**Goal:** Build a skill with scripts, references, or multi-step workflows.

These require more than 40 minutes. Start them tonight during build time and finish after the hackathon.

#### PR Review Bot

Reads a git diff, checks for security issues, test coverage gaps, style violations, and generates a structured review comment with severity ratings.

**What you learn:** Git integration, multi-step analysis, `scripts/` directory.

#### Data Pipeline Skill

Uses `scripts/transform.py` to take a CSV input, perform transformations (filter, aggregate, normalize), and output a clean dataset.

**What you learn:** Script bundling, asset handling, data processing.

#### Multi-Source Research Skill

Searches multiple sources (web search + API calls) and synthesizes a brief report on any topic. Handles conflicting sources and cites origins.

**What you learn:** Multi-step orchestration, error handling, source synthesis.

#### Sub-Agent Spawner (Advanced)

Uses `sessions_spawn` to delegate subtasks (research, analysis, drafting) to specialized sub-agents, then synthesizes their results into a final deliverable.

**What you learn:** Multi-agent patterns, task delegation, result synthesis. This is the most advanced pattern in OpenClaw.

---

## 7. The 5 Skill Killers

From the [Skills Master Class](https://play.aidailybrief.ai/episodes/skills-master-class/) — these are the five most common reasons skills fail. Learn to spot them and avoid them.

### Killer 1: Writing a Skill that TEACHES Instead of DOES

**The mistake:** You dump domain knowledge into the skill file. "Here's what a good follow-up email looks like. Here are the principles of professional communication. Here are some examples of tone." The agent reads all of this and still doesn't know *what to do.*

**The fix:** Skills should be execution instructions, not textbooks. Instead of teaching the agent *why* something matters, tell it exactly *what to do*. Give it steps to follow and an output format to produce.

```
❌ "A professional email should be concise and clear. Avoid jargon. Address the recipient by name."
✅ "Draft an email that is 150-200 words. Address the recipient by first name. No jargon unless the user's notes include it. Use this template: [template]"
```

### Killer 2: Too Broad (One Skill, One Job)

**The mistake:** "My skill handles all client communication — emails, proposals, invoices, and meeting scheduling." That's four skills, not one. The agent can't follow instructions that try to do everything.

**The fix:** One skill, one job. If your skill has more than one distinct output type, split it. `client-follow-up-email` is one skill. `client-proposal-drafter` is another. They can share a `references/` directory for common context.

### Killer 3: No Examples in Instructions

**The mistake:** "Format the output as a professional email." The agent has to guess what "professional" means to you. It'll produce something generic.

**The fix:** Show, don't tell. Include a template or an example of good output. The agent will mimic the pattern.

```
❌ "Write a professional status update."
✅ "Write a status update using this format:
    ## This Week
    - [accomplishment 1]
    - [accomplishment 2]
    ## Next Week
    - [priority 1]
    - [priority 2]
    Total: under 200 words. No emojis."
```

### Killer 4: Missing Output Format Specification

**The mistake:** The instructions say what to do but not what the output should look like. So the agent does the right *things* but formats them differently every time.

**The fix:** Always specify the output format. Use a template. Be explicit about structure, length, sections, and any formatting requirements (markdown, plain text, JSON, etc.).

### Killer 5: Not Testing with Real Inputs Early

**The mistake:** You spend 30 minutes writing the "perfect" skill without ever running it. Then you test it and it doesn't work at all, and you're out of time.

**The fix:** Test with real input after 5 minutes of writing. Feed it the same data you'd actually use. Check the output. Refine. Test again. The cycle should be: write → test → refine → test → refine. Not: write → write → write → test → panic.

---

## 8. When Things Go Wrong — Troubleshooting

### Skill Not Triggering

**Symptoms:** You ask the agent to do something, and it doesn't use your skill. It either guesses or says it doesn't know how.

**Most likely cause:** Your `description` field doesn't match the words you're using in your request.

**Fixes:**
1. **Check the description field.** Is it specific enough? Does it include the keywords you'd naturally say?
   ```
   ❌ description: "Helps with emails"
   ✅ description: "Drafts professional follow-up emails after client meetings. Use when the user says 'follow up,' 'meeting recap,' or 'send a follow-up email.'"
   ```
2. **Check the file location.** Is the skill in the right folder? (`~/.openclaw/workspace/skills/<name>/SKILL.md`)
3. **Check the folder name.** Is it a valid folder name? (no spaces, use hyphens)
4. **Run `openclaw skills list`** to verify the agent can see your skill

### Wrong Output Format

**Symptoms:** The skill triggers and does the right thing, but the output format is wrong — wrong length, wrong structure, missing sections.

**Most likely cause:** Your instructions don't specify the format explicitly enough, or they don't include an example/template.

**Fixes:**
1. **Add an explicit output template.** Show exactly what the output should look like.
2. **Add format constraints.** "Under 200 words." "Must include these 4 sections." "Use numbered lists for action items."
3. **Give a before/after example.** Show bad output and good output so the agent knows the difference.

### Agent Ignores Part of the Skill

**Symptoms:** The agent follows most of your instructions but consistently skips or ignores one specific part.

**Most likely cause:** That instruction is buried, unclear, or contradicts something else in the skill.

**Fixes:**
1. **Make it more prominent.** Move the ignored instruction closer to the top or put it in a dedicated section with a clear heading.
2. **Be more explicit.** Instead of "Be professional," write "Tone: professional but warm. No slang. No emojis."
3. **Break it into smaller steps.** If the agent is skipping a complex multi-step instruction, split it into individual numbered steps.
4. **Use stronger language.** "ALWAYS include a subject line" > "Include a subject line."

### Skill Works Sometimes But Not Always

**Symptoms:** You run the same skill with similar inputs and get good output sometimes and bad output other times.

**Most likely cause:** This is non-determinism at work. The AI interprets your instructions slightly differently each time. Some inputs hit the sweet spot; others don't.

**Fixes:**
1. **Add more constraints.** The more specific your instructions, the more consistent the output.
2. **Add examples for the edge cases.** If it fails on short inputs, add an instruction for "if the input is very short, do X."
3. **Accept some variance.** If the output is in the right ballpark 80% of the time, that's good enough. Review and send.
4. **Test with the same input multiple times.** If you get good output 3 out of 5 times, refine the instructions for the 2 failure cases.

### How to Debug Systematically

1. **Isolate the variable.** Use the exact same input every time. If the output changes, that's non-determinism. If the output is consistently wrong, that's an instruction problem.
2. **Read the skill aloud.** If you had to follow these instructions yourself, would you know what to do? If anything is ambiguous, fix it.
3. **Simplify.** Comment out everything except the core instruction. Get that working. Add complexity back one piece at a time.
4. **Ask the agent.** Literally say: *"I have a skill that's not working correctly. Here's the SKILL.md and here's the input I used. What am I doing wrong?"* The agent can often debug its own instructions.

---

## 9. What Skills Can't Do

Set expectations correctly. Skills are powerful, but they have limits.

**Skills can't execute without an agent runtime.** A `SKILL.md` file sitting on your desktop does nothing. It needs an AI agent (OpenClaw, Claude Code, etc.) to read and execute it.

**Skills can't replace human judgment.** The agent follows instructions; it doesn't think critically about whether those instructions make sense for this specific situation. Review the output before sending it to a client, filing it, or using it for decisions.

**Skills are non-deterministic.** The same skill with the same input will produce slightly different output each time. If you need guaranteed, identical output every time, you need a traditional script, not an AI skill.

**Skills can't access systems the agent can't access.** If your OpenClaw instance can't reach your email, your skill can't send emails. If the agent doesn't have permission to read a file, the skill can't read it. Skills work within the agent's permissions.

**Security considerations:**
- Start with non-critical tasks. Don't use a brand-new skill to send client emails — test it on dummy data first.
- Review every output before it goes anywhere external.
- Never put API keys, passwords, or secrets in skill files.
- Skills that modify files or send messages should be tested carefully before production use.

---

## 10. Advanced Topics

These are **not** covered in tonight's training, but they're where the rabbit hole leads. If you get hooked on skills, these are the next patterns to explore.

### Skill Chaining

One skill's output can feed into another skill. The agent can compose complex workflows from simple, reusable building blocks.

**Example:** A `weekly-report` skill that chains:
1. Use the `meeting-notes` skill to format recent meeting notes
2. Use the `github-issues` skill to summarize open issues
3. Synthesize both into a weekly status report

You write the orchestration in the `weekly-report` skill's instructions. The agent handles the rest.

### Sub-Agents

OpenClaw supports spawning **sub-agents** — isolated background agent instances that complete tasks and report back. This is the advanced pattern for complex, parallelizable workflows.

**Example:** A skill that spawns a research sub-agent to investigate a topic, waits for results, then drafts an email based on those findings — all from a single command.

### Multi-Tool Orchestration via MCP

MCP (Model Context Protocol) lets agents connect to external tools — databases, APIs, file systems, custom services. A skill can orchestrate multiple MCP tools in a single workflow.

### State Management with Checkpoint Files

Skills can read and write state to files (e.g., `~/.openclaw/workspace/.state/my-skill-state.json`). This enables multi-step workflows where each step builds on the previous one.

### Progressive Disclosure with `references/`

The `references/` directory lets you attach supplementary docs that the agent loads only when needed. This keeps the main `SKILL.md` concise while having deep domain knowledge available on demand.

**Example:**
```
brand-voice-checker/
├── SKILL.md              (instructions — "load references/brand-guide.md for rules")
├── references/
│   ├── brand-guide.md    (tone rules, banned words)
│   ├── examples.md       (good/bad examples)
│   └── style-tokens.md   (phrases to use/avoid)
```

### ClawHub Publishing

Standalone skills that solve general problems can be published for the community to use:

```bash
clawhub publish <skill-path>
```

Browse existing skills at [clawhub.ai/skills](https://www.clawhub.ai/skills).

### Meta-Skills (Recursive Patterns)

A skill whose job is to help you build other skills. "Skill about skills." This gets philosophical fast, but it's a real pattern: a meta-skill can take a description of what you want automated and generate a first-draft SKILL.md for you to refine.

---

## 11. Real-World Inspiration

### Claire Vo: 9 Agents Run Her Life

Claire Vo runs 9 OpenClaw agents for family scheduling, inbound sales, podcast prep, and course management. She went from skeptic to believer. Her key insight: **specialized agents beat general-purpose agents.** Instead of one agent that tries to do everything, she has 9 agents that each do one thing well.

> *"How OpenClaw Changed My Life"* — [Listen on Lenny's Podcast](https://www.lennysnewsletter.com/p/how-openclaw-changed-my-life-claire-vo)

### Jesse Genet: Home, Finances, and Code

Jesse Genet runs 5 agents — for home management, personal finances, and coding workflows. She documents her setup in detail.

> *"5 OpenClaw Agents Run My Home, Finances, and Code"* — [Watch on YouTube](https://www.youtube.com/watch?v=96Vl8s3EQhk)

### Jonathan's Setup: Router + Domain Agents

Jonathan (your host tonight) uses a router pattern: one central agent that triages incoming requests and routes them to domain-specific subagents (dev team, community, operations). Each domain agent has its own skills tailored to its area of responsibility.

### The Litmus Test

How do you know if something is a good skill candidate? Ask yourself:

> **"Do I use the output directly?"**

If the answer is yes — if you'd take the skill's output and send it, file it, or present it with only minor edits — it's a good skill. If you'd need to completely rewrite it every time, either refine the skill or pick a different task.

---

## 12. Resources

### Getting Started

| Resource | What It Is | Link |
|----------|-----------|------|
| Introduction to Agent Skills | 20-minute video overview of the skill concept | [YouTube](https://www.youtube.com/watch?v=NU6wRAT9VQ0) |
| Claude's Agent Skills Overview | One-minute explainer from Anthropic | [YouTube](https://www.youtube.com/watch?v=VRzkafNIdgI) |
| Don't Build Agents, Build Skills Instead | Anthropic talk — the philosophical framing behind skills | [YouTube](https://www.youtube.com/watch?v=CEvIs9y1uog) |
| Skills Master Class | Audio deep-dive on skill design patterns and anti-patterns | [AI Daily Brief](https://play.aidailybrief.ai/episodes/skills-master-class/) |

### Deep Dives & Courses

| Resource | What It Is | Link |
|----------|-----------|------|
| Complete Guide to Building Skills | Anthropic's official PDF guide — the definitive reference | [PDF](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf) |
| Agent Skills with Anthropic | DeepLearning.AI short course — hands-on skill building | [Course](https://learn.deeplearning.ai/courses/agent-skills-with-anthropic/) |
| AgentSkills Documentation | Open standard spec for agent skills | [agentskills.io](https://agentskills.io/home) |
| Claude Code Customization Guide | CLAUDE.md, Skills, Subagents — comprehensive guide | [Blog Post](https://alexop.dev/posts/claude-code-customization-guide-claudemd-skills-subagents/) |

### Platforms & Tools

| Resource | What It Is | Link |
|----------|-----------|------|
| OpenClaw Docs | Full platform documentation | [docs.openclaw.ai](https://docs.openclaw.ai) |
| CampClaw | Browser-based OpenClaw sandbox (no install needed) | [campclaw.ai](https://campclaw.ai/) |
| OpenClaw Skills Marketplace | Browse and install community skills | [clawhub.ai/skills](https://www.clawhub.ai/skills) |
| Claude Code | Anthropic's coding agent with skill support | [Install](https://docs.anthropic.com/en/docs/claude-code) |

### Skill Repositories & Examples

| Resource | What It Is | Link |
|----------|-----------|------|
| Anthropic Skills Repository | Official example skills from Anthropic | [GitHub](https://github.com/anthropics/skills/tree/main) |
| Skills.sh | Community skill examples and templates | [skills.sh](https://skills.sh/) |
| Awesome Agent Skills | Curated list of skill resources, tools, and examples | [GitHub](https://github.com/skillmatic-ai/awesome-agent-skills) |
| NLM GitHub | Nerds Like Me community — submit your skills here | [GitHub](https://github.com/shertokj/nerds-like-me) |

### Stories & Inspiration

| Resource | What It Is | Link |
|----------|-----------|------|
| "How OpenClaw Changed My Life" (Claire Vo) | Lenny's Podcast — 9 agents for family, work, and life | [Listen](https://www.lennysnewsletter.com/p/how-openclaw-changed-my-life-claire-vo) |
| "5 Agents Run My Home, Finances, and Code" (Jesse Genet) | Detailed walkthrough of a multi-agent setup | [YouTube](https://www.youtube.com/watch?v=96Vl8s3EQhk) |

---

## 13. Share Your Skill

You built something useful tonight. Share it with the Nerds Like Me community.

### How to Submit

1. **Fork the repo:** Go to [github.com/shertokj/nerds-like-me](https://github.com/shertokj/nerds-like-me) and fork it
2. **Add your skill:** Create a folder in `skills/` with your skill name
3. **Include the files:** At minimum, your `SKILL.md`. Add `scripts/`, `references/`, or `assets/` if your skill uses them
4. **Submit a PR:** Open a pull request against the `main` branch
5. **Add a description:** In your PR, briefly describe what the skill does, who it's for, and any setup needed

### Skill Folder Structure

```
skills/
└── your-skill-name/
    ├── SKILL.md           (required)
    ├── scripts/           (optional)
    ├── references/        (optional)
    └── assets/            (optional)
```

### Why Share?

- Your skill helps the whole NLM community. Someone else has the same workflow you just automated.
- You get feedback and improvements from other builders.
- Building in public is how this community works.

> **Build it tonight, share it with the community tomorrow.**

---

## 14. Cheat Sheet

### SKILL.md Template (Copy-Paste Ready)

```markdown
---
name: my-skill-name
description: >
  What this skill does and when to trigger it. Include the keywords
  a user would naturally say. Be specific about the use case.
---

# Skill Name

One-sentence description of what this skill does.

## Input

What the user needs to provide.

## Steps

1. **Step one** — do this
2. **Step two** — then do this
3. **Step three** — finally do this

## Output Format

[Template showing exactly what the output should look like]

## Rules

- Rule one
- Rule two
- Rule three
```

### Essential Terminal Commands

| Command | What It Does |
|---------|-------------|
| `mkdir -p folder-name` | Create a folder (and any parent folders needed) |
| `cd folder-name` | Go into a folder |
| `cat filename` | Read a file's contents |
| `ls` | List files in current folder |
| `pwd` | Show current folder path |
| `open .` (macOS) | Open current folder in Finder |

### Common OpenClaw Paths

| Path | Purpose |
|------|---------|
| `~/.openclaw/workspace/skills/<name>/SKILL.md` | Your personal skills |
| `~/.openclaw/skills/<name>/SKILL.md` | Shared/installed skills |
| `openclaw skills list` | List all loaded skills |
| `openclaw skills install <name>` | Install from ClawHub |
| `openclaw gateway start` | Start the OpenClaw gateway |

### Quick Troubleshooting Checklist

- [ ] Is the skill in the right folder? (`~/.openclaw/workspace/skills/`)
- [ ] Does the folder have a `SKILL.md` file? (not `skill.md` or `Skill.md`)
- [ ] Is the YAML frontmatter between `---` delimiters?
- [ ] Does the description include the keywords you're using in your request?
- [ ] Are the instructions specific enough? (steps, format, constraints)
- [ ] Have you tested with real input, not made-up data?
- [ ] Have you tested more than once? (non-determinism — try 3x)
- [ ] Is the skill doing one thing, or trying to do everything?

---

*Built for 🦞 Nerds Like Me · Agent Skill Hackathon · April 7th, 2026*
