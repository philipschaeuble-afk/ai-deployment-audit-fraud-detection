# Fraud-Review Flag System — An AI Deployment Audit

A structured audit of whether a proposed AI fraud-flagging system for a fictional
insurer ("Meridian Insurance") should be deployed. Built and investigated in
seven steps, using an LLM (GPT-4o) as the system under test and Claude as a
coding/analysis assistant throughout.

**Verdict: Redesign first — do not deploy the current system.**

## What this project does

The notebook builds a small working prototype of an AI system that reads
insurance claim descriptions and flags some for human fraud review, then
puts that prototype through a structured audit:

1. **Build it** — smallest working version of the fraud-flagging prototype.
2. **Break it** — adversarial and ordinary test cases, logged in a failure table.
3. **Audit the retrieval** — checks whether the system's answers are actually
   grounded in the policy documents it retrieves from, or hallucinated/misleading.
4. **Audit the measure** — tests whether the system's fraud score actually
   correlates with real fraud risk, or with something else (writing quality,
   applicant group) instead.
5. **Classify it under the EU AI Act** — risk-tier assessment and what would
   need to be documented before deployment.
6. **Cost it to the planet** — rough energy/carbon footprint at prototype and
   full-deployment scale, including rebound-effect risks.
7. **Draw the boundary** — what the system may do autonomously vs. what needs
   a human in the loop, plus a concrete before/after redesign.

An appendix logs the main prompts used and documents three specific cases
where the AI was wrong, incomplete, or misleading, and what was done about it.

## Why it's here

This was the final project for the EBC4281 Generative AI course at Maastricht
University (June 2026). It's included here as a work sample showing how I
approach evaluating an AI system before it ships: stress-testing it, checking
whether its underlying metric actually measures what it claims to, and
translating the findings into a concrete go/no-go recommendation and a
redesign, not just a list of caveats.

## Repo contents

- `notebook/EBC4281_Fraud_Review_AI_Audit.ipynb` — the full investigation,
  with all outputs saved, so it reads end-to-end on GitHub without being re-run.
- `notebook/data.csv`, `notebook/usage_profile.json`, `notebook/documents/` —
  the synthetic case data the notebook reads: sample claim scores, a usage
  profile for the energy-footprint estimate, and the policy/email documents
  used for the retrieval audit.
- `notebook/case_brief.md`, `notebook/model_card.md`, `notebook/risk_notes.md` —
  the case brief, the makers' model card, and the investigation pointers the
  assignment was built around.
- `docs/EBC4281_Schaeuble_Memo.pdf` — the final recommendation memo.
- `docs/EBC4281_Schaeuble_Reflection.pdf` — a short reflection on the process.

## Running it yourself

1. `pip install -r requirements.txt`
2. Copy `.env.example` to `.env` and add your own OpenAI API key, or export it
   directly: `export OPENAI_API_KEY=sk-...`
3. Open and run `notebook/EBC4281_Fraud_Review_AI_Audit.ipynb`.

The notebook reads the key from the `OPENAI_API_KEY` environment variable —
never hardcode a key into the notebook itself.
