# Workshop prompts (the live build, in order)

Setup before the room fills:
- Demo chat: a NEW, clean Project / Gem in the assistant you demo with. Web search ON. No customer data, nothing private.
- Second window: Claude Code in an EMPTY folder. Never inside a real repo.
- Optional: Claude in Chrome in a clean Chrome profile (nothing logged in) for the slide 6 demo.
- Hotspot as Wi-Fi backup. Font size up in every window.

Prompts 1-5 run in the SAME chat, because each builds on the last.
Prompt 0 runs in the SECOND window right after the room picks the idea (slide 3).

Fallback idea if the room is quiet (rehearse this one end to end):
> Freelancers and small agencies lose time and cash chasing unpaid invoices. They want to see who owes them what, and send polite reminders without awkwardness.

---

## Slide 3: right after the vote, paste this ONE line into the demo chat

The chosen idea: [the room's idea in 1-2 sentences, in their words]. Every following task is about this idea.

Then immediately: prompt 0 in the second window, prompt 1 in the demo chat.

---

## 0. Background build (second window, Claude Code)

Create a new project called "idea-prototype" in this folder.
Goal: a clickable, multi-screen web prototype for user testing of this idea: [the room's idea].
First plan the 3-4 most important screens (one of them an empty state), describe each in one line, then build them.
Data: 20 made-up sample records that look realistic. No real data.
Tech: the simplest thing that runs in a browser and starts with one command. English UI, short friendly copy, clean light design.
Write a README: how to start it, what is in it, what is not (no real backend).
Work on your own and only ask if you are stuck. When it runs locally, deploy it to Vercel as a public production deployment (vercel deploy --prod --yes) and check that the link opens without a login. Then make a QR code of that link as a PNG and open it. The data is made up, so the link is safe to share.
At the end, give me the local link, the public link and the QR file.

---

## 1. Research: real customer words (starts during the talk, read it at slide 29)

Role: a senior product researcher.
Context: the idea above.
Task:
1. Search public sources for what real users say about the problem and about the existing solutions: app store reviews, G2 / Capterra reviews, Reddit and forum threads.
2. Group the complaints into 5-7 themes.
3. For every theme: how often it came up in what you found, 2 verbatim quotes, each with its link.
4. Name the 3-5 existing solutions people mention, and what they like and hate about each.
5. Top 3 opportunities: what I would build first and why (frequency × pain).
Format: one table of themes, then at most 10 bullets.
Check: only use what you actually found. Every quote needs a link. If something cannot be found, write "no data". Do not invent numbers.

### 1b. Verify (open 2-3 links live)

List every quote behind the top theme with its link. Mark any you could not open again.

### 1c. Ideas with evidence

Based on the themes, give 5 feature ideas for a first version. For each: one sentence, which quotes back it up (link), and expected impact (small / medium / large). In a table.

---

## 2. Business case

Role: a product manager and a financial analyst in one.
Context: the chosen idea and the research above. Target: small businesses and freelancers.
Task: write a simple business case.
1. What problem does it solve, for whom? (2-3 sentences)
2. Impact hypotheses (for example: time saved, faster payment, conversion to paid).
3. Assumptions table: assumption | pessimistic | base | optimistic | how we would validate it.
4. Estimated result for the 3 scenarios, with the calculation steps shown.
5. Risks (including data protection) and what we would measure in a 2-week test.
Format: tables + at most 8 bullets.
Check: clearly mark what is an assumption and what is a fact from the research. Do not invent market data; where it would be needed, write "to validate".

### 2b. Spreadsheet

Turn the assumptions table and the calculation into a Google Sheets layout with formulas, so I can change any assumption and the result updates.

---

## 3. Spec from the room

Ask 3-4 people one question each and type (or dictate) their answers as raw notes:
1) Who hurts most from this?  2) What is the minimum without which it is worthless?  3) What could go wrong?  4) How will we know it works?

Notes from the room:
[raw notes here]

Role: an experienced product manager.
Task: from the notes above and the chosen idea, write a one-page spec:
- Problem and who it hurts (quote the notes)
- Goal and success metric
- In scope / out of scope
- User stories (at most 5)
- Acceptance criteria in Given / When / Then
- Edge cases (at least 6)
- Open questions, and who can decide them
Check: anything not in the notes goes under open questions, do not make it up.

### 3b. Red team (slide 30, the most valuable step)

Review this spec through four pairs of eyes: 1) a skeptical engineer, 2) the customer who says no and would never pay, 3) an investor, 4) a bank's risk and compliance officer (customer data, regulation, fraud). Each writes the 3 biggest gaps or risks. Then update the spec and list what changed.

### 3c. Tasks (only if there is time)

Break it into tasks as CSV: title, description, acceptance criterion, size (S/M/L), dependency.

---

## 4. Prototype with references (slide 31)

Paste 2-3 screenshots of apps the room admires (or from Mobbin) into the chat first.

Build a clickable mobile prototype (a single HTML page) from the spec:
- the main overview or list screen with 6-10 realistic made-up records,
- a detail view,
- settings, if the feature needs them,
- an empty state.
Use the attached screenshots as the visual reference: spacing, type sizes, density, tone. Do not copy their brand.
Make three variants side by side on one page (A, B, C) that differ in layout, not just colour.
This is a prototype for user testing, not production code.

### 4b. Iterate with the room

Ask: "Which one, and what should we change?" Type what they say:
We pick variant [A/B/C]. Change: [the room's request]. Show only that variant from now on.

### 4c. Write the taste down (slide 32)

From the chosen variant, write a short design-rules.md: colours (with hex), font family and sizes, spacing scale, corner radius for controls and for cards, what is banned (for example gradients, heavy shadows), and a rule that every screen has an empty state. At most 15 lines. I will attach this file to every future design request.

---

## 5. Launch kit

From the final spec, write a launch kit:
1. Release note (max 60 words)
2. Three versions of a push or email subject line (max 60 characters)
(If there is time: a help article with steps and 4 FAQs, and a support reply for the most likely question.)
Tone: friendly, short sentences, no hype.

### 5b. Measurement (optional, not run live)

1. Success metrics: 1 main + 3 supporting, and what counts as success after 4 weeks.
2. Event tracking plan in a table: event name, when it fires, properties.
3. One SQL query or spreadsheet formula for the main metric.

Then: reveal the background build in the second window. "This wasn't a question, it was a task."

---

## 6. Ops automation example (slide 33, show, don't run)

Shown as a scheduled task (Claude Cowork scheduled task, or a ChatGPT scheduled task with connectors):

Every weekday at 8:00:
1. Read new emails in the support inbox from the last 24 hours.
2. Group them by topic and write a 5-line summary for me.
3. Draft a reply to each one, using the tone and answers in my "support-rules" file. Do NOT send anything.
4. Create a ticket for every bug report, with the customer's words quoted.
5. List anything urgent at the top.
Anything that sends, pays or deletes waits for my approval.

---

## 7. The task you hate most

Slide 34. Everyone in the room does this one.

I want to hand a task I hate to AI. The task: [describe it in 2-3 sentences].
Interview me with 5 short questions, one at a time, about how I do it today, what good output looks like, and what must never go wrong.
Then write: 1) the steps as a checklist, 2) the instructions for a Project / Gem that does it with me, 3) what I still check myself every time.
