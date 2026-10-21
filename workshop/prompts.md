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
Tech: plain HTML, CSS and JavaScript in a few files, no npm install, no build step; it starts with `python3 -m http.server`. English UI, short friendly copy, clean light design.
Write a README: how to start it, what is in it, what is not (no real backend).
Work on your own and only ask if you are stuck. When it runs locally, deploy it to Vercel as a public production deployment (vercel deploy --prod --yes) and check that the link opens without a login. Then make a QR code of that link as a PNG (with the qrencode tool already installed on this machine) and open it. The data is made up, so the link is safe to share.
At the end, give me the local link, the public link and the QR file.

---

## 1. Research: real customer words (starts during the talk, read it at slide 29)

Role: a senior product researcher.
Context: the idea above.
Task:
1. Search public sources for what real users say about the problem and about the existing solutions: app store reviews, G2 / Capterra reviews, Reddit and forum threads. Prefer reviews of existing products. Leave out posts and comments from people building or selling a tool; count them separately as "vendor".
2. Group the complaints into 5-7 themes.
3. For every theme: how often it came up (the number of separate posts or reviews you opened, no percentages), 2 verbatim quotes of at most 20 words, each with its link. Mark each quote (opened) if you read it on the page itself, or (snippet) if it only came from a search result. Sites that refuse to open: write "blocked". Aim for 8-12 quotes in total.
4. Name the 3-5 existing solutions people mention, and what they like and hate about each.
5. Top 3 opportunities: what I would build first and why (frequency × pain).
Format: one table of themes, then at most 10 bullets, then a 3-line summary I can read aloud.
Check: only use what you actually found. Every quote needs a link. If something cannot be found, write "no data". Do not invent numbers.

### 1b. Verify (open 2-3 links live)

List every quote behind the theme you ranked first in the opportunities, with its link. Mark any you could not open again.

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
6. Verdict: Go, Narrow or Stop, and the one test result that would change it.
Format: tables + at most 8 bullets.
Check: clearly mark what is an assumption and what is a fact from the research. Do not invent market data; where it would be needed, write "to validate".

### 2b. Spreadsheet (optional, not in the timed flow)

Turn the assumptions table and the calculation into a Google Sheets layout with formulas, so I can change any assumption and the result updates.

---

## 3. Spec from the room

Ask 3-4 people one question each and type (or dictate) their answers as raw notes:
1) Who hurts most from this?  2) What is the minimum without which it is worthless?  3) What could go wrong?  4) How will we know it works?

Notes from the room:
[raw notes here]

Role: an experienced product manager.
Task: from the notes above and the chosen idea, write a one-page spec. Start with the v0.1 scope in one line, and what was cut.
- Problem and who it hurts (quote the notes)
- Goal and success metric
- In scope / out of scope
- User stories (at most 5)
- Acceptance criteria in Given / When / Then
- Edge cases (at least 6)
- Open questions, and who can decide them
Check: anything not in the notes goes under open questions. You may propose concrete values for acceptance criteria and edge cases; mark each one (proposed) and repeat it under open questions.

### 3b. Red team (slide 30, the most valuable step)

Review this spec through four pairs of eyes: 1) a skeptical engineer, 2) the customer who says no and would never pay, 3) an investor, 4) a bank's risk and compliance officer (customer data, regulation, fraud). Each writes the 3 biggest gaps or risks. Then update the spec and list what changed.

### 0b. Update the background build (second window, right after 3b)

Here is the final spec after the red team:
[paste the updated spec]
Update the prototype in idea-prototype to match it, deploy again to the same project, and list in at most 5 bullets what changed.

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
Use the attached screenshots as the visual reference: spacing, type sizes, density, tone. Do not copy their brand. If no screenshots are attached, say so and go light and calm.
Make three variants side by side on one page (A, B, C) that differ in layout, not just colour.
Share the data and the CSS across the three variants; keep the whole page under 400 lines. This is a prototype for user testing, not production code.

### 4b. Iterate with the room

Ask: "Which one, and what should we change?" Type what they say:
We pick variant [A/B/C]. Change: [the room's request]. Show only that variant from now on.

### 4c. Write the taste down (slide 32)

From the chosen variant, write a short design-rules.md. Read every value from the variant's code and add nothing that is not there: colours (with hex), font family and sizes, spacing scale, corner radius for controls and for cards, what is banned (for example gradients, heavy shadows), and a rule that every screen has an empty state. At most 15 lines. I will attach this file to every future design request.

---

## 5. Launch kit

From the final spec, write a launch kit:
1. Release note (max 60 words)
2. Three versions of a push or email subject line (max 60 characters)
(If there is time: a help article with steps and 4 FAQs, and a support reply for the most likely question.)
Tone: friendly, short sentences, no hype.
Check: only what the prototype does today. No data-protection or security claims unless the room decided them.

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

---

## After the workshop (not in the live build)

Five prompts for the rest of the week, same shape as the live ones: role, context, task, format, check. Each one drafts; you read it, fix it and send it yourself. Customer interviews, pricing, a first sales message, partners and the weekly numbers are already in [guides/succeed.md](../guides/succeed.md) and on the handout, so they are not repeated here.

### 8. After a sales call: the follow-up

Role: a founder-led sales assistant.
Context: my raw notes (or the transcript) from a call with [name, role, company]. [paste]
Task: draft the follow-up email I send today.
Format: one line thanking them for something specific they said; their problem in their own words (one quote); what we agreed, at most 3 bullets; the next step with a date and who does it. Under 150 words. Below the email, separately: anything they asked that I did not answer.
Check: promise nothing that is not in my notes, and no feature that does not exist today. If the notes have no agreed next step, say so instead of inventing one.

### 9. The monthly investor update

Role: my chief of staff.
Context: this month's numbers [paste], what went well, what went badly, what I need help with. Last month's update: [paste, or "this is the first one"].
Task: draft this month's investor update in the short early-stage format Elad Gil recommends: asks first, then highlights, lowlights, milestones ([Investor Update Emails](https://blog.eladgil.com/p/investor-update-emails)).
Format: asks at the top, at most 3, each concrete enough that one person could act on it (a named kind of company, a role to hire, a specific intro); 1-2 key numbers vs last month; 2-5 highlights; 2-5 lowlights; next month's milestones.
Check: the lowlights stay in, in plain words. Every number matches what I pasted, with the calculation shown for any derived one. Flag any ask too vague to act on ("intros to customers").

### 10. Competitor teardown

Role: a skeptical market analyst.
Context: my product in one paragraph: [...]. The competitor: [name, website].
Task: a teardown from public sources only: their site, pricing page, docs, changelog, app store and review sites.
Format: a table: who they sell to | what it does | price and plan structure | what customers praise | what customers complain about, every cell with a link and the date you saw it. Then 3 places we are clearly better, 3 where they are, and one question to ask our next customer about them.
Check: praise and complaints are verbatim quotes, marked (opened) or (snippet) as in prompt 1. Anything you cannot find is "not public", not a guess. No claims about their revenue or customer count unless a source says it.

### 11. Meeting notes into decisions and owners

Role: a meticulous note-taker.
Context: the transcript or my rough notes from [meeting]. [paste]
Task: turn it into a record someone who was not there can act on.
Format: decisions made (one line each, who decided); actions (what, owner, due date); open questions; anything discussed but left undecided.
Check: an action without an owner or a date is listed as "no owner" or "no date"; do not assign one. A suggestion nobody agreed to is not a decision. Quote where the exact wording matters.

### 12. Contract first read (not legal advice)

Role: a careful reader preparing me for a conversation with my lawyer. You are not my lawyer and this is not legal advice.
Context: a contract I am asked to sign: [type, my side, the other side]. [paste or attach]
Task: help me understand what I would be agreeing to and what to ask.
Format: 1) a 5-line plain-English summary; 2) a table: clause (section number and a short quote) | what it means for me | unusual or one-sided? | question for my lawyer. Cover at least term and termination, payment, liability caps, indemnities, IP ownership, data protection, auto-renewal, exclusivity; 3) the 3 questions I should ask first.
Check: every point quotes the clause with its section number. A clause you would expect but cannot find is "not found". Do not tell me whether to sign.

Before you paste a contract, check that your tool's data settings allow it (a business or team plan, with training on your data turned off). Anything that binds you to money, liability or IP still gets a real lawyer; this prompt makes that meeting shorter, not unnecessary.
