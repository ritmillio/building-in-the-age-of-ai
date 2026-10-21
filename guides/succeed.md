# Succeed: validate, price, sell, stay small

A prototype takes an afternoon now. That moves the hard part: knowing it is worth building, getting someone to pay, and staying alive long enough to find out. This guide is the go-to-market half of the workshop. Each section has a short rule, the source it rests on, and a prompt you can paste.

Links checked 2026-10-21. Where a claim is ours (what we do), it says "we". Where it is someone else's, it links to them. For raising money and the "thin wrapper" problem, see [fundraising.md](fundraising.md).

The prompts use the same five-part brief as the live build ([prompts.md](../workshop/prompts.md)): role, context, task, format, check. The check line matters most: "no data" and "to validate" are allowed answers.

---

## 1. Validate before you build

**Talk about their life, not your idea.** Rob Fitzpatrick's [The Mom Test](https://www.momtestbook.com/) boils customer interviews down to three habits: talk about their life instead of your idea, ask about specifics in the past instead of opinions about the future, and talk less and listen more. Compliments and "I would definitely use that" are not data. What someone did last month, and what it cost them, is. YC's [How to Talk to Users](https://www.youtube.com/watch?v=MT4Ig2uqjTc) (Eric Migicovsky, Y Combinator) is the same idea in a short talk.

AI helps on both sides of the conversation: before (a sharp interview guide) and after (an honest synthesis that keeps the customer's own words). It does not replace the conversation. Write each conversation down in the same shape: [interview-notes.md](../templates/interview-notes.md).

```text
Role: a customer researcher who has read The Mom Test.
Context: I am exploring [problem] for [who]. I will talk to 5 of them this week.
Task: write a 20-minute interview guide. Only questions about what they did in the past and what it cost them. No question that mentions my idea or asks "would you use".
Format: 8 questions max, each with one follow-up ("Tell me about the last time...").
Check: flag any question that invites a compliment or a guess about the future, and rewrite it.
```

```text
Role: a skeptical researcher.
Context: below are my raw notes from [N] customer conversations. [paste]
Task: synthesise them.
Format: 1) problems ranked by how often they came up and what they cost, each with a verbatim quote and who said it; 2) what they do today instead; 3) what surprised me; 4) what I still don't know.
Check: quote, don't paraphrase. Mark anything I seem to want to hear but nobody actually said. If fewer than 3 people said it, say so.
```

**Mine what customers already wrote.** Reviews, forum threads and support complaints about the tools your customers use today are interviews someone else already did. Prompt 1 of the live build ([Research: real customer words](../workshop/prompts.md#1-research-real-customer-words-starts-during-the-talk-read-it-at-slide-29)) does this with web search on, quotes with links, and "no data" allowed. *Fails when:* you let it summarise without quotes; you get its opinion, not theirs.

**Test the promise before the product.** Before writing Buffer, Joel Gascoigne put up a page describing it, then added a pricing page between the description and the email sign-up, so each visitor had to pick a plan first ([Buffer: idea to paying customers in 7 weeks](https://buffer.com/resources/idea-to-paying-customers-in-7-weeks-how-we-did-it/)). People kept signing up and a few clicked paid plans: enough evidence to build. With AI the page takes minutes; the slow part is sending real people to it.

```text
Role: a conversion copywriter.
Context: [one paragraph: who, problem, the promise]. Real customer quotes: [paste 3-5].
Task: write a one-page landing page that sells this promise to [who], plus a pricing section with 2-3 plans, and a sign-up that says "we're not live yet, leave your email and we'll tell you first".
Format: headline, subhead, 3 benefits in the customer's words, plans, sign-up.
Check: no feature that does not exist in the spec; no invented testimonials or numbers.
```

**Red team it before the market does.** Ask for the four people who will say no: the engineer, the customer who would never pay, the investor, the risk officer. Prompt 3 in [prompts.md](../workshop/prompts.md#3-spec-from-the-room) has the exact wording. *Fails when:* you only fix the gaps that are cheap to fix.

## 2. Decide with a number, not a feeling

**Write the business case as scenarios.** Pessimistic, base, optimistic, each assumption with how you would validate it, ending in Go, Narrow or Stop and the one test result that would change the verdict. That is prompt 2 in [prompts.md](../workshop/prompts.md#2-business-case). The point is not the forecast; it is the list of assumptions you now know to test.

**Ask the product-market-fit question early.** Superhuman asked its users "How would you feel if you could no longer use Superhuman?" with three answers (very, somewhat, not disappointed). Sean Ellis, who benchmarked nearly a hundred startups with this survey, found that companies where at least 40% answered "very disappointed" were the ones that grew ([First Round Review](https://review.firstround.com/how-superhuman-built-an-engine-to-find-product-market-fit/)). Superhuman added three questions: who benefits most, what the main benefit is, how to improve it. You can run it with ten users.

```text
Role: a product analyst.
Context: answers to the four-question product-market-fit survey from [N] users. [paste]
Task: 1) the share answering "very disappointed"; 2) describe the people who answered "very disappointed" (role, situation) in their own words; 3) the main benefit they name; 4) what "somewhat disappointed" users say holds them back.
Format: one table + 5 bullets.
Check: show the counts behind every percentage. Under 10 answers, say the number is not reliable yet.
```

## 3. Price it

**You are probably charging too little.** In YC's [Startup Pricing 101](https://www.youtube.com/watch?v=jwXlo9gy_k4) (Kevin Hale; also on the [YC library](https://www.ycombinator.com/library/6h-startup-pricing-101)), consistently under-charging is the number one thing he tells startups to fix. Price against the value to the customer, not against your cost, and treat each price as an experiment: record conversion and revenue at each price you try.

**Ask about money in the interview, not after the build.** "What do you pay for this today, in money or hours?" is a past-tense question and passes the Mom Test. "Would you pay 20 euros?" does not.

**Borrow a pricing skill instead of improvising.** Corey Haines's MIT-licensed [`pricing`](https://github.com/coreyhaines31/marketingskills/tree/main/skills/pricing) skill covers tiers, packaging and the value metric; install steps and other marketing skills are in [skills/third-party.md](../skills/third-party.md).

```text
Role: a pricing advisor for early-stage B2B products.
Context: who pays: [role, company size]. What it replaces today and what that costs them: [from interviews]. Competitors and their public prices: [or "research them, with links"].
Task: propose 2-3 plans with a value metric (per seat, per document, per outcome), and the price for each.
Format: table: plan | who it's for | what's included | price | why this price.
Check: every competitor price has a link and a date. Price from the customer's value and today's cost, not from my cost. List what I should ask in the next 3 sales conversations to test it.
```

**If you sell an AI product, know your cost per task.** Your margin moves with usage, and a cheap per-token model can be an expensive task. Measure it ([trick 66](tricks.md)) before you set a flat price.

## 4. The first ten customers

**Do it by hand.** Paul Graham, [Do Things that Don't Scale](https://paulgraham.com/ds.html): "The most common unscalable thing founders have to do at the start is to recruit users manually." His example is the Collison brothers at Stripe, who would say "Right then, give me your laptop" and set the product up on the spot.

**Start with your network, then go where they already are.** Lenny Rachitsky looked at how fast-growing B2B companies found their [first ten customers](https://www.lennysnewsletter.com/p/how-todays-fastest-growing-b2b-businesses): almost all combined their personal network (former colleagues, investors, friends) with going to where their customers already spend time (communities, forums, door to door). His verdict on press: "Getting press is rarely the way to get started." The consumer version is [How the biggest consumer apps got their first 1,000 users](https://www.lennysnewsletter.com/p/how-the-biggest-consumer-apps-got).

**AI drafts, you send.** Let it research the account and draft the message. You read every word, fix what sounds generic, and press send yourself. Generic AI outreach is easy to spot and costs you the one chance you had.

```text
Role: a founder-led sales assistant.
Context: my product: [one paragraph]. The person: [name, role, company, link]. How I know them or why them: [...].
Task: research their company (public sources, with links) and draft a short first message.
Format: 3 facts about their situation with links, then a message under 90 words that mentions one specific thing about them and asks for a 20-minute conversation about how they handle [problem] today. No pitch.
Check: no fact without a link. Nothing I could not say face to face. I send it, you don't.
```

## 5. Sell through people who already have their trust

**Find who your customers already listen to.** Small businesses take advice from their accountant, their bank, their industry association, the software they already pay for. One partner who recommends you can reach more of the right people than a year of ads, and the trust carries over. This is also part of the moat answer in [fundraising.md](fundraising.md#2-the-wrapper--moat-debate): distribution you already have beats distribution you hope for.

```text
Role: a partnerships lead.
Context: my customer: [who]. The problem: [...]. What they use and who they ask for advice today: [from interviews].
Task: list the 10 most promising partner types (not companies yet) who already have this customer's trust, and for the top 3: what they gain from recommending us, what it costs them, and the first email to one of them.
Format: table + 3 short emails.
Check: every "they gain" is a concrete benefit to the partner (less work, happier clients, revenue share), not "innovation". Mark guesses as guesses.
```

*Fails when:* the partner gains nothing. "Your clients will love it" is not a reason for a busy accountant.

## 6. Stay small on purpose

**Know whether you are default alive.** Paul Graham, [Default Alive or Default Dead?](https://paulgraham.com/aord.html): with expenses constant and revenue growing at its recent rate, does the money you have get you to profitability? Ask it every month. Paste your numbers and ask an assistant to do the arithmetic with the steps shown; do not let it guess growth.

**Hire the work to agents before you hire people.** Teams are smaller than they used to be, and some reach real revenue with a few dozen people ([fundraising.md, smaller teams](fundraising.md#smaller-teams-faster-revenue)). Start with the task you hate most ([prompt 7](../workshop/prompts.md#7-the-task-you-hate-most)), give it two weeks, keep or drop it. Repeat. Anything that sends, pays or deletes still waits for a human.

**Raising is a choice.** Some founders raise once, get profitable and keep control. Read [fundraising.md](fundraising.md) before you decide.

## 7. The few numbers that matter early

Before revenue is large, a handful of numbers tell you more than any dashboard:

- **The "very disappointed" share** from section 2, and who those people are.
- **Retention:** are the people who started a month ago still using it? Ask the agent to compute it from your sign-up and activity data, and to show the query.
- **Time to first value:** how long from sign-up to the first useful result. AI products live or die here.
- **Revenue per customer and gross margin,** with model costs included ([fundraising.md, margins](fundraising.md#margins-and-inference-cost)).
- **Months of runway** at current spend: the default alive test.

a16z's [16 Startup Metrics](https://a16z.com/16-startup-metrics/) defines the standard ones precisely if an investor asks.

```text
Role: my weekly operating analyst.
Context: this week's raw numbers: sign-ups, active users, paying customers, revenue, model/API spend, cash. [paste or connect]
Task: a one-screen weekly update.
Format: table of this week vs last week vs 4 weeks ago; then 3 bullets: what moved, why it might have moved, what I should look at.
Check: show the calculation for every derived number. If a number is missing, write "missing", don't estimate. No adjectives like "strong" or "healthy".
```

---

## Reading list

- Rob Fitzpatrick, [The Mom Test](https://www.momtestbook.com/). Two hours; the best book on customer conversations.
- Eric Migicovsky, [How to Talk to Users](https://www.youtube.com/watch?v=MT4Ig2uqjTc) (YC video).
- Kevin Hale, [Startup Pricing 101](https://www.youtube.com/watch?v=jwXlo9gy_k4) (YC video).
- Paul Graham, [Do Things that Don't Scale](https://paulgraham.com/ds.html) and [Default Alive or Default Dead?](https://paulgraham.com/aord.html).
- First Round Review, [How Superhuman Built an Engine to Find Product/Market Fit](https://review.firstround.com/how-superhuman-built-an-engine-to-find-product-market-fit/).
- Lenny Rachitsky, [first ten B2B customers](https://www.lennysnewsletter.com/p/how-todays-fastest-growing-b2b-businesses) and [first 1,000 consumer users](https://www.lennysnewsletter.com/p/how-the-biggest-consumer-apps-got).
- Joel Gascoigne, [Idea to paying customers in 7 weeks](https://buffer.com/resources/idea-to-paying-customers-in-7-weeks-how-we-did-it/).
- a16z, [16 Startup Metrics](https://a16z.com/16-startup-metrics/).

More from this repo: [tricks.md](tricks.md) (how we build), [war-stories.md](war-stories.md) (what went wrong), [fundraising.md](fundraising.md) (raising money and moats).
