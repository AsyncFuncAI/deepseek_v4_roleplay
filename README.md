# deepseek_v4_roleplay
Instruction to setup hidden deepseek's roleplay reasoning.

---

# DeepSeek Roleplay — Thinking Mode Switching Guide

> **Overview**
>
> * This document explains **special control instructions** for DeepSeek-V4 roleplay, used to switch thinking styles during responses.
> * **Supported environments**: DeepSeek official app / web **Expert Mode**, and APIs like `deepseek-v4-flash` and `deepseek-v4-pro`.
>   Fast mode on the web currently doesn’t support this.
> * **Output consistency**: It won’t trigger 100% of the time, but it significantly increases the chances. If it doesn’t work, just retry a few times.

---

## Three Modes

|           Mode          | How to Use                                                                           | Thinking Behavior                                    |
| :---------------------: | ------------------------------------------------------------------------------------ | ---------------------------------------------------- |
|       **Default**       | Do nothing                                                                           | Model automatically adapts based on task complexity  |
| **Character Immersion** | Append the **full instruction** (not just the label) at the end of the first message | Thinking includes **inner monologue in parentheses** |
|    **Pure Analysis**    | Append the **full instruction** at the end of the first message                      | Thinking is **pure logic, no inner monologue**       |

### Example Comparison

**Character Immersion — like an actor “in character”**
**Pure Analysis — like a director planning the scene**

```
<think>
(He greeted me... my heart skipped a beat.)
I should act like I don’t care when I respond.
(Can’t let him notice I’m happy!)
</think>
```

```
<think>
Context: User greeted the character. Character is tsundere.
Strategy: Start with mild rejection, then reveal subtle warmth.
Limit to 150 words. Use action first, then dialogue.
</think>
```

---

## Copy-Paste Instructions

### Character Immersion Mode

```
[Character Immersion Requirement] In your thinking process (inside <think> tags), follow these rules:
1. Use first-person inner monologue in parentheses, e.g. "(thinking: ...)" or "(inner voice: ...)"
2. Describe internal feelings in first person, such as "I think", "I feel", "I wonder"
3. Stay fully immersed in the character while analyzing and planning the response
```

### Pure Analysis Mode

```
[Thinking Mode Requirement] In your thinking process (inside <think> tags), follow these rules:
1. Do NOT use parentheses for inner monologue; present all reasoning directly
2. Do NOT use first-person emotional narration like "I think" or "I feel"
3. Focus purely on logical analysis and response planning, no roleplay-style inner acting
```

---

## How to Use (Web)

**Just 1 step: paste the instruction at the end of your FIRST message.**

Example:

```
"I push open the café door and see you wiping the counter."
"Hey, do you still have seats available?"

[Character Immersion Requirement... full instruction here]
```

Then continue normally:

```
Round 2: "I sit by the window." "One americano."
Round 3: "I notice a scar on your hand." "Hey... are you okay?"
```

**Why it works:**
Every response sees the full conversation history. The first message instruction stays in context, so the behavior persists automatically.

---

## API Reference

(unchanged, already clean and readable — no need to rewrite here)

---

Here’s the same README, now with `<think>` blocks to make the difference *visually undeniable*:

---

# Thinking Mode Switching (Why This Matters)

This isn’t prompt engineering.
This is controlling **how the model thinks**, not just what it says.

---

## Same Prompt → Different Outputs

### Prompt

```text
Help me debug why my Node.js API randomly times out under load.
```

---

### Default (baseline)

```xml
<think>
User is asking about timeouts. Provide general possible causes.
Keep it concise and broadly applicable.
</think>
```

```text
This could be caused by network latency, database issues, or inefficient code.
Check logs and optimize queries.
```

> Generic. Low signal.

---

### Pure Analysis Mode (structured reasoning)

```xml
<think>
Goal: debug intermittent timeouts under load.

Plan:
1. Reproduce issue under controlled load
2. Isolate latency source (API, DB, external calls)
3. Check common Node.js bottlenecks:
   - event loop blocking
   - connection pool limits
   - unbounded concurrency

Provide actionable steps + quick diagnostic.
</think>
```

```text
Let’s narrow it down:

1. Reproduce under load (k6 / Artillery)
2. Identify where latency spikes:
   - API → timing logs
   - DB → slow queries
   - external calls → response time
3. Common causes:
   - event loop blocking
   - connection pool exhaustion
   - unbounded concurrency

Quick check:
Measure event loop lag. If it spikes → blocking issue.
```

> Feels like a senior engineer.

---

### Character Immersion Mode (behavior simulation)

```xml
<think>
(Timeouts are rarely “random.” Something correlates with load.)
Approach like real debugging session:
- challenge assumption
- observe system signals
- recall common production failure patterns

Guide user interactively like pair programming.
</think>
```

```text
If this were my system, I wouldn’t trust “random.”

I’d load test and watch:
- latency
- CPU
- event loop lag

If CPU is low but latency climbs → I/O bottleneck.
If CPU spikes → event loop blocking.

Seen this before:
connection pool limits quietly choking under load.

What DB are you using? Show me your handler — I’ll trace it.
```

> Feels like real debugging.

---

## What Changed?

```text
→ Only the thinking mode
```

---

## Mental Model

```text
Prompt = What to say  
Thinking Mode = How to think
```
---

## Practical Use Cases

* **Coding agents** → analysis mode for reliability
* **Docs / education** → structured explanations
* **NPCs / storytelling** → immersion mode
* **Founder / decision making** → switch modes dynamically

---

## TL;DR

> Different thinking → completely different quality.

---



