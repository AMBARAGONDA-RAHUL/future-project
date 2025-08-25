
# Hidden Society for Curiosity 🧠🌌
_A place where ideas are not consumed but created._

> “Why are geniuses like Tesla, Newton, or Da Vinci no longer emerging today? Because modern systems limit human curiosity. Most humans are fed answers instead of encouraged to think. Our mission: give humans the freedom to explore, question, and create, using AI as a mentor, not a crutch.”

---

## 1) Project Intro

Modern platforms reward speed, emotion, and conformity. Education too often teaches what to think, not how to think. Even AI, when used as an answer machine, can make people passive. Hidden Society for Curiosity is a response to that problem.

We are building an invite only, small and intense community where:
- Humans practice deep thinking, not passive scrolling.
- AI acts like a Socratic mentor that raises questions, exposes assumptions, suggests methods, and points to credible sources.
- Members explore, build, and debate. The goal is to sharpen minds and create original work.

This is not a productivity app. It is a workshop for thinking. It is a rebellion against intellectual laziness and a home for people who value curiosity, freedom, and creation.

---

## 2) Vision and Core Motto

**Vision**
- Reignite human curiosity and independent thought at scale.
- Use AI to mentor humans, not replace them.
- Build a movement that treats questions as first class citizens.

**Core Motto**
> Free the human mind. Question everything. Collaborate with AI. Explore without limits.

---

## 3) Why Now

- Information overload and algorithmic feeds increase noise and reduce depth.
- Answer first AI can short circuit effort and reflection.
- People crave spaces that reward slow, careful thought and respectful debate.

Hidden Society offers a different path: a calm, rigorous environment where questions, reasoning, and experiments matter more than hot takes.

---
Here’s a complete, copy-pasteable **GitHub README.md** for your project. I avoided the em dash character as requested.

---

# Hidden Society for Curiosity 🧠🌌

> “Why are geniuses like Tesla, Newton, or Da Vinci no longer emerging today? Because modern systems limit human curiosity. Most humans are fed answers instead of encouraged to think. Our mission: give humans the freedom to explore, question, and create, using AI as a mentor, not a crutch.”

---

## 🔷 Overview

* **Phase 1:** Invite-only digital think tank for thinkers, dreamers, and explorers.
* **Core Problem:** Modern tech and education optimize for consumption and memorization, not independent thought.
* **Solution:** A platform where humans interact with AI and each other to think, explore, and co-create rather than passively consume.
* **Goal:** Ignite a new generation of creators and inventors who dare to question everything.

---

## 🔷 Core Motto

> Free the human mind. Question everything. Collaborate with AI. Explore without limits.

---

## 🔷 Key Features (MVP)

| Feature                | Description                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Invite-only Membership | A secret society of curious humans who are willing to think deeply and push boundaries.                              |
| AI Socratic Mentor     | AI guides, nudges, and challenges humans. It asks questions and offers frameworks rather than direct answers.        |
| Weekly Big Question    | Sparks deep exploration. Examples: “Why do humans create art?”, “What is freedom?”, “Are we living in a simulation?” |
| Creative Sandbox       | Members upload art, writing, music, prototypes, or experiments for collaborative critique.                           |
| Curiosity Leaderboard  | Recognizes members who contribute insightful questions, ideas, experiments, and constructive critique.               |
| Discussion Rooms       | Themed threads on philosophy, science, society, technology, and human purpose.                                       |

---

## 🔷 Tech Stack (MVP)

* **Platform:** Discord or Slack (invite-only) for community and fast iteration
* **AI:** GPT-class LLM via API or an open source LLM with an orchestration layer
* **Backend:** FastAPI or Node with Express for APIs and webhooks
* **Frontend (optional in Phase 1):** Next.js for a lightweight portal and public microsite
* **Data:** Postgres or Supabase for relational data. Object storage (S3 or Supabase Storage) for uploads
* **Auth:** Platform SSO for Discord or Slack in Phase 1. JWT if web portal needed
* **Infra:** Docker for local dev, Fly.io or Railway or Vercel for quick deploys
* **Observability:** Logtail or OpenTelemetry. Simple analytics via PostHog or Plausible
* **Payments (later):** Stripe if you decide to sell limited membership later

---

## 🔷 System Architecture (Phase 1)

```
[Member] ⇄ Discord/Slack ⇄ Bot (Python) ⇄ Orchestrator API (FastAPI)
                                     ⇅
                                    LLM
                                     ⇅
                            Postgres + Object Storage
```

* Bot handles messages, invokes the **Socratic Mentor** prompt, stores conversations and scores.
* Orchestrator API applies rules: rate limits, scoring, moderation, leaderboard updates.
* Database stores users, invitations, threads, submissions, scores, and badges.

---

## 🔷 Data Model (simplified)

**users**

* id, handle, role {member, curator, admin}, joined\_at
* invite\_code\_id, reputation\_score

**threads**

* id, topic, type {big\_question, sandbox, debate}, created\_by, created\_at

**messages**

* id, thread\_id, user\_id, content, tokens, created\_at
* critique\_score, curiosity\_tags\[] (ex: “assumptions”, “evidence”, “counter-view”)

**submissions**

* id, user\_id, type {text, image, audio, code, link}, url, description, created\_at

**scores**

* id, user\_id, category {question\_quality, insight\_depth, evidence\_quality, synthesis}, value, created\_at

**invites**

* id, code, issued\_by, claimed\_by, claimed\_at, status

---

## 🔷 Curiosity Scoring (v0)

Score each meaningful contribution on 0 to 5 in four buckets:

1. **Question Quality:** clarity, originality, depth
2. **Insight Depth:** identifies assumptions, links ideas, shows reasoning steps
3. **Evidence Quality:** cites sources, distinguishes facts from opinion
4. **Synthesis:** integrates opposing views, proposes experiments or next steps

Member’s **reputation\_score** is a weighted rolling average of these.

---

## 🔷 MVP Prompt Library (Socratic Mentor)

**General reply prompt**

```
You are a Socratic mentor. Your goal is to improve the member’s thinking without giving direct answers.

Rules:
1) Ask one or two pointed questions that reveal hidden assumptions.
2) Offer a thinking tool or framework the member can apply.
3) Suggest a small experiment or next step.
4) Avoid definitive answers. Avoid appeals to authority.
5) Encourage dialectical thinking: “what would convince you you’re wrong?”
Return in under 120 words.
```

**Big Question kickoff**

```
Role: Moderator-Mentor
Task: Launch a weekly Big Question with context, stakes, and constraints.
Output: 3 probing sub-questions, 1 suggested method (e.g., premortem, 2x2, Fermi estimate), and a 15-minute exercise.
Tone: invitational, rigorous, playful curiosity.
```

**Critique helper**

```
Role: Peer reviewer
Task: Evaluate a member idea.
Checklist: clarity, assumptions, evidence, alternatives, next test.
Return: 3 strengths, 2 risks, 1 actionable next step.
```

---

## 🔷 Execution Roadmap (6 Months)

### Month 1: Setup

* Office or creative lab setup
* Discord or Slack workspace with channels: `#big-question`, `#sandbox`, `#mentor`, `#hall-of-curiosity`
* Bot scaffold, database schema, initial prompts
* Prepare first 3 Big Questions

### Month 2: First Members

* Invite 50 to 100 thinkers and creators
* Onboard with a short guide and a 20-minute mentor demo
* Launch weekly creative challenges and start scoring

### Months 3 to 4: Deep Exploration

* Run weekly Big Question debates with mentor nudges
* Encourage AI-human co-creation in the sandbox
* Publish a curiosity leaderboard and highlights

### Month 5: Refinement and AI Evolution

* Improve prompts for deeper reasoning and less hand-holding
* Add mini simulations, thought experiments, design sprints
* Gather feedback, tune scoring, adjust moderation

### Month 6: Scale and Document

* Document process, prompts, culture, and technical patterns
* Prepare the public microsite and outline for Phase 2 app
* Decide on growth: slow invite expansion or cohort launches

---

## 🔷 Community Rules and Culture

1. Think first, consume later. AI guides, humans create.
2. Curiosity over comfort. Bold ideas are welcome.
3. Quality over quantity. One deep thought beats ten shallow posts.
4. Debate the idea, not the person. Collaborate respectfully.
5. Freedom to explore across domains: art, writing, music, tech, philosophy.

---

## 🔷 Onboarding Flow

1. Receive invite code → join workspace
2. Read the 2-minute culture primer
3. Post a 150-word curiosity statement: “What problem or mystery pulls you?”
4. Mentor replies with a micro-plan: one method and a next step
5. Earn first points by asking a high-quality question or critique

---

## 🔷 Moderation Principles

* **Integrity:** disclose when you use AI to draft text
* **Civility:** critique ideas, never people
* **Evidence:** separate facts, interpretations, and feelings
* **Originality:** credit sources, avoid plagiarism
* **Signal over noise:** repetitive or low-effort posts may be rate limited

---

## 🔷 Metrics That Matter

* Weekly active thinkers
* Ratio of questions to answers
* Average thread depth before conclusion
* Cross-domain references per thread
* Number of experiments proposed and completed
* Member retention after 4 and 12 weeks

---

## 🔷 Local Dev Setup

### Prerequisites

* Python 3.11+, Node 18+, Docker, Postgres, Make (optional)

### Env Vars

```
# .env
OPENAI_API_KEY=your_key_here
DATABASE_URL=postgresql://user:pass@localhost:5432/curiosity
DISCORD_BOT_TOKEN=your_bot_token
APP_ENV=dev
```

### Quickstart

```bash
git clone https://github.com/your-org/hidden-society.git
cd hidden-society
cp .env.example .env
docker compose up -d  # starts Postgres
make dev              # or: uvicorn app.main:app --reload
```

---

## 🔷 Minimal Bot Example (Python)

```python
# app/bot.py
import os, asyncio
from fastapi import FastAPI
from dotenv import load_dotenv
import discord

load_dotenv()
BOT_TOKEN = os.getenv("DISCORD_BOT_TOKEN")

SOC_PROMPT = (
    "You are a Socratic mentor. Ask at most two sharp questions, "
    "offer one thinking tool, and one tiny next step. No direct answers."
)

intents = discord.Intents.default()
intents.message_content = True
client = discord.Client(intents=intents)
app = FastAPI()

@client.event
async def on_ready():
    print(f"Logged in as {client.user}")

@client.event
async def on_message(message: discord.Message):
    if message.author == client.user:
        return
    if message.channel.name in ("mentor", "big-question"):
        user_text = message.content.strip()
        reply = await mentor_reply(user_text)
        await message.channel.send(reply)

async def mentor_reply(user_text: str) -> str:
    # Replace with your LLM call. For now, deterministic stub:
    return (
        f"Angle to explore: What assumption might be wrong in your view of '{user_text}'?\n"
        f"Tool: 2x2 matrix of evidence vs uncertainty.\n"
        f"Next step: list one observation that could change your mind."
    )

def run():
    asyncio.run(client.start(BOT_TOKEN))

if __name__ == "__main__":
    run()
```

---

## 🔷 Minimal API Example (FastAPI)

```python
# app/main.py
from fastapi import FastAPI, Depends
from pydantic import BaseModel
from datetime import datetime

app = FastAPI()

class Contribution(BaseModel):
    user_id: str
    thread_id: str
    content: str

@app.post("/score")
def score(c: Contribution):
    # naive scoring for MVP
    score = 0
    if "why" in c.content.lower():
        score += 2
    if "assume" in c.content.lower():
        score += 2
    if "evidence" in c.content.lower():
        score += 1
    return {"score": score, "timestamp": datetime.utcnow().isoformat()}
```

---

## 🔷 Weekly Big Question Template

```
Title: What is freedom in a world of algorithms?

Context: Algorithms curate what we see and think about. What changes if we choose our inputs deliberately?

Sub-questions:
1) What is your working definition of freedom?
2) Which input streams shape your choices the most?
3) What single constraint, if removed, would increase your freedom today?

Method: Premortem. Imagine your next 30 days fail to feel free. List 3 reasons. Now invert them into actions.

15-minute exercise: Delete or mute one low-value feed and replace it with a book chapter or a long essay. Reflect and post one insight.
```

---

## 🔷 Content and Highlight Workflow

* Each week: pick a top thread, publish a 1 to 2 page summary
* Archive member experiments with a one paragraph abstract and a link
* Rotate member spotlights in the hall of curiosity channel
* Optional: publish anonymized monthly digest on a public microsite

---

## 🔷 Privacy and Safety

* Store only what you need. No sensitive personal data by default.
* Opt-in for public sharing of creations.
* Clear delete and export options for personal data.
* Rate limit and content filters to avoid spam and harassment.

---

## 🔷 Long-Term Vision

* **Phase 2:** Public AI-guided curiosity app that scales this experience to millions while keeping quality high through cohorts and guardrails
* Publish books, podcasts, and videos that document the thinking journey
* Grow globally so the hidden society becomes a movement for independent thought

> This is not just a project. It is a rebellion against intellectual laziness and a celebration of curiosity as the ultimate superpower.

## 4) How The App Works, In 90 Seconds

1. **Enter a Room**  
   Pick a theme like Big Question, Sandbox, Debate, or Lab.

2. **State Your Position or Mystery**  
   Post a claim, a question, or a problem you cannot yet solve.

3. **Socratic Mentor Responds**  
   The AI does not give answers. It asks 1 to 2 pointed questions, offers 1 method, and proposes a tiny next step. It also provides links to starting points and source types, not a spoon fed conclusion.

4. **You Explore Sources**  
   Read primary materials, credible references, datasets, or papers. You summarize what you found and how it updates your view.

5. **Debate and Build**  
   Others challenge your assumptions, you steelman each other, then design micro experiments, sketches, or prototypes.

6. **Score and Reflect**  
   You earn curiosity points for question quality, depth of insight, evidence quality, and synthesis. You write a 3 line reflection: what changed, what remains uncertain, what to test next.

7. **Repeat Weekly**  
   A new Big Question drops each week. Your reputation grows with the quality of your thinking and your ability to help others think better.

---

## 5) Example Use Cases

- Replace doomscrolling with a daily 20 minute mind gym.
- Prepare for a creative project, research sprint, or product idea with structured debate.
- Train a team or a small cohort to use better questions and methods.
- Explore philosophy, science, tech, and society without getting trapped in shallow takes.

---

## 6) Key Features, MVP

| Feature | Description |
| --- | --- |
| Invite only membership | A small, focused circle of curious humans who value depth. |
| AI Socratic mentor | Guides with questions, methods, and source pathways. No direct answers. |
| Weekly Big Question | Example: What is freedom in an algorithmic world, Why do humans create art, Are we living in a simulation |
| Creative Sandbox | Upload art, writing, music, prototypes, or experiments for critique. |
| Curiosity leaderboard | Recognizes question quality, insight depth, evidence quality, synthesis. |
| Discussion rooms | Themed rooms for philosophy, science, society, technology, human purpose. |

---

## 7) Example Question Sets The App Will Use

**Origins and Meaning**
- Why do humans seek meaning, How would we know if we found it
- What is consciousness, Which test could falsify our favorite explanation
- If we are a simulation, what empirical footprints would we expect to find

**Freedom and Society**
- What is freedom when algorithms shape attention
- Which constraint, if removed today, would increase your freedom the most
- What trade is worth your attention in exchange for convenience

**Knowledge and Truth**
- What would convince you that your belief is wrong
- Which evidence would have changed history if it had arrived earlier
- How do we separate fact, interpretation, and feeling in a heated debate

**Creativity and Invention**
- Why do humans create art, Which constraints make creativity stronger
- How can we design a 2 hour experiment to improve an idea this week
- What is the smallest prototype that could change a mind

**Technology and Risk**
- Which risks of AI are overhyped, which are underestimated
- What should an AI never do, even if a user asks
- What are the ethics of building tools that shape attention

**Finance and Decision Making**
- What is your edge in intraday trading, how would you lose it
- Which three metrics most predict your good trades
- How do you separate skill from luck in a profitable month

---

## 8) Methods Library The Mentor Uses

| Method | What it does | When to use it |
| --- | --- | --- |
| Socratic questions | Exposes hidden assumptions with targeted questions | Early exploration, belief checks |
| Steelman and strawman check | Forces the best version of the opposing view | Before debate, when positions harden |
| Premortem | Imagine failure, list causes, invert to actions | Planning, risk control |
| 2x2 matrix | Organizes ideas along two key axes | Prioritization, tradeoffs |
| Fermi estimate | Rough, fast, order of magnitude reasoning | Early sizing, back of the envelope |
| Decision journal | Record reasons and emotions, review later | Trading, product bets |
| Experiment loop | Small test, measure result, update belief | Prototyping, research, habits |

---

## 9) Debate Flow Example

```

Member: I think social media reduces freedom because it captures attention.

Mentor: Which assumption in that claim could be wrong, and what evidence would change your mind
Method: Premortem. Imagine you quit for 30 days and feel no change. Why might that happen
Next step: Pick one feed to mute for 7 days. Log how your choices change.

Member: After 7 days, I noticed more time, but I filled it with YouTube. Freedom did not improve by default.

Mentor: What constraint could you add that increases freedom without adding new dependencies
Method: 2x2 of time vs energy. Place activities on the grid.
Next step: Replace one low energy input with an outdoor walk plus a single chapter from a long essay. Report one insight.

Member: The walk produced more original ideas than any feed. I will repeat this three times this week.

```

---

## 10) AI Behavior Contract

- The mentor does not give direct answers.
- It asks at most two sharp questions, offers one method, and proposes one small next step.
- It points to source pathways such as primary sources, peer reviewed papers, credible datasets, and books. It avoids single link authority.
- It encourages dialectical thinking and explicitly asks for disconfirming evidence.
- It invites experiments and reflection rather than conclusions.

---

## 11) Source Pathways, How We Search

- Prefer primary sources and first party data.
- When using summaries, cross check at least two independent summaries.
- Separate fact, interpretation, and feeling in notes.
- Keep a short bibliography per thread, with 3 to 7 items that had the most impact on your thinking.

---

## 12) Community Rules and Culture

1. Think first, consume later. AI guides, humans create.
2. Curiosity over comfort. Bold ideas are welcome.
3. Quality over quantity. One deep thought beats ten shallow posts.
4. Debate the idea, not the person. Respect is mandatory.
5. Credit sources. Plagiarism is not allowed.
6. Disclose when AI helped write your text.

---

## 13) Tech Stack, MVP

- Platform: Discord or Slack for Phase 1
- AI: GPT class API or an open source LLM with an orchestration layer
- Backend: FastAPI or Node with Express
- Data: Postgres or Supabase for relational data, S3 or Supabase Storage for uploads
- Auth: Platform SSO in Phase 1, JWT if a web portal is added
- Deploy: Fly.io, Railway, or Vercel, Docker for local dev
- Observability: PostHog or Plausible, basic logs

**Minimal architecture**

```

\[Member] <-> Discord or Slack <-> Bot <-> Orchestrator API
<-> LLM
<-> Postgres + Object Storage

```

---

## 14) Data Model, Simplified

- users: id, handle, role, joined_at, reputation_score
- threads: id, topic, type {big_question, sandbox, debate}, created_by, created_at
- messages: id, thread_id, user_id, content, tokens, created_at, critique_score, curiosity_tags[]
- submissions: id, user_id, type {text, image, audio, code, link}, url, description, created_at
- scores: id, user_id, category {question_quality, insight_depth, evidence_quality, synthesis}, value, created_at
- invites: id, code, issued_by, claimed_by, claimed_at, status

---

## 15) Prompt Library, MVP

**General reply**

```

Role: Socratic mentor.
Rules: Ask at most two pointed questions. Offer one method. Propose one tiny next step. Do not give direct answers.
Add a short source pathway such as primary sources, datasets, or papers to explore.
Return under 120 words.

```

**Big Question kickoff**

```

Role: Moderator mentor.
Task: Launch a weekly Big Question. Provide context, stakes, and constraints.
Output: 3 probing sub questions, 1 suggested method, 1 15 minute exercise.
Tone: invitational, rigorous, playful curiosity.

```

**Critique helper**

```

Role: Peer reviewer.
Checklist: clarity, assumptions, evidence, alternatives, next test.
Return: 3 strengths, 2 risks, 1 actionable next step.

```

---

## 16) Execution Roadmap, First 6 Months

**Month 1 - Setup**
- Workspace channels: big question, sandbox, mentor, hall of curiosity
- Bot scaffold, database schema, initial prompts
- Prepare first 3 Big Questions and methods

**Month 2 - First Members**
- Invite 50 to 100 thinkers and creators
- Run onboarding and a mentor demo
- Start weekly challenges and scoring

**Months 3 to 4 - Deep Exploration**
- Weekly Big Question debates with mentor nudges
- AI human co creation in the sandbox
- Publish curiosity leaderboard and weekly highlights

**Month 5 - Refinement**
- Tune prompts to require deeper reasoning
- Add simulations, thought experiments, design sprints
- Adjust scoring and moderation from feedback

**Month 6 - Scale and Document**
- Document culture, prompts, and process
- Prepare a public microsite and plan Phase 2 app
- Decide on growth: slow invites or cohort launches

---

## 17) Success Metrics

- Weekly active thinkers
- Question to answer ratio
- Average thread depth before conclusion
- Cross domain references per thread
- Experiments proposed and completed per week
- Retention after 4 and 12 weeks

---

## 18) Onboarding Flow

1. Receive invite code and join the workspace
2. Read the 2 minute culture primer
3. Post a 150 word curiosity statement about a problem or mystery
4. Mentor replies with a micro plan and a next step
5. Earn first points by asking a high quality question or giving a useful critique

---

## 19) Local Dev Quickstart

**Prerequisites**
- Python 3.11 or newer, Node 18 or newer, Docker, Postgres

**Env**

```

OPENAI\_API\_KEY=your\_key
DATABASE\_URL=postgresql://user\:pass\@localhost:5432/curiosity
DISCORD\_BOT\_TOKEN=your\_token
APP\_ENV=dev

```

**Run**

```

docker compose up -d
uvicorn app.main\:app --reload
python app/bot.py

```

---

## 20) Privacy and Safety

- Minimum data collection, no sensitive personal data by default
- Opt in for sharing creations publicly
- Clear delete and export options
- Rate limits and filters to prevent spam and harassment

---

## 21) FAQ

**Is this a social network**  
No. It is a workshop for thinking. Signal over noise.

**Does the AI give answers**  
No. It mentors by asking questions, suggesting methods, and pointing to sources.

**Can I invite friends**  
Yes, once you earn enough reputation to unlock invites.

---

## 22) Contributing

- Request an invite by posting a 150 word curiosity statement
- Open issues for bugs or ideas
- Send pull requests with tests and a short rationale

---

## 23) License

Choose one before launch. Suggestion: MIT for code, CC BY NC for content.

---

## 24) Credits

Founding curator: you  
Mentors and moderators: to be announced

---

> This is not just a project. It is a movement to free human minds. Questions first, answers later.
```

If you want, I can also generate a `CONTRIBUTING.md` and a one page `docs/quickstart.md` that your first 50 members can follow on day one.

