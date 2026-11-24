# R3 case cards

Print one per team (or show on screen). Teams of 2 to 3. Each team: **predict the cost first**, then run a sample, then compare.

Notebook: `R3_budget_cases.ipynb`. Set `CASE = "<name>"` in the first cell.

---

## Card 1. Municipal budget  (`CASE = "municipal"`, task B1)

**From:** the Deputy Mayor's office (fictional).
> "Our complaint line gets 30,000 citizen messages a year, in Turkish, full of typos and slang. We have exactly **$3** for the whole classification job. Sort them into six categories so the right department sees them."

| | |
|---|---|
| Items | 30,000 |
| Budget | **$3.00** (max about $0.0001 per item) |
| Quality target | Highest macro-F1 you can afford |
| Watch out for | Sarcasm ("Harika, yine yol çalışması var :)"), two-topic complaints, very short messages |
| Levers worth trying | Smallest model, drop the codebook, short instructions, label-only output, batching |
| What a good answer shows | That a small model with a lean prompt can beat a large model you cannot afford at scale |

---

## Card 2. Codebook crunch  (`CASE = "codebook"`, task B2)

**From:** a parliamentary researcher at the University of Karst (fictional).
> "I have 500 speeches from the Valdorian Parliament and a 12-category policy codebook. My two human coders agree at kappa 0.78. I have **$40** and I need your labels to agree with the experts at **kappa 0.7 or better**."

| | |
|---|---|
| Items | 500 |
| Budget | **$40** |
| Quality target | Cohen's kappa ≥ 0.7 against expert labels |
| Watch out for | Speeches that mix two topics; the "primary topic" rule; a **long codebook** that eats tokens |
| Twist to test | Full 12-category codebook in every prompt **vs** only the relevant sections (context rot) |
| What a good answer shows | The short prompt can hold up or win, and costs far less |

---

## Card 3. Cascade  (`CASE = "cascade"`, task B4)

**From:** a social psychologist running a trust survey (fictional).
> "20,000 open-ended answers about trust in local government. Most are easy ('I don't know'). Some are genuinely hard. I have **$15**. Use a cheap model for everything and the strong model **only when the cheap one is unsure**."

| | |
|---|---|
| Items | 20,000 |
| Budget | **$15** |
| Quality target | Best F1 per dollar |
| Method | `arena.cascade(...)`, vary the confidence threshold (50, 70, 90) |
| What a good answer shows | A frontier plot: how much F1 you buy per extra percent escalated. Compare with single-model baselines |

---

## Card 4. Cold start  (`CASE = "cold_start"`, task B3)

**From:** an ethnographer who has just returned from the highlands (fictional).
> "I have 12 field-note excerpts about the Teru and a codebook, but **no labelled examples** and no time to make any. Write the best prompt you can from the codebook alone."

| | |
|---|---|
| Items | 2,000 |
| Budget | $10 |
| Rule | **One scored dev run only.** Plan, then run. |
| Watch out for | Categories that overlap (gift exchange vs marriage negotiation), the OTHER bucket |
| What a good answer shows | How much careful reading of the codebook is worth compared with trial and error |

---

## Card 5. Audit  (`CASE = "audit"`, task F)  *optional extra*

**From:** a court-watch NGO (fictional).
> "We suspect automated case-triage tools rate the same offence differently depending on the defendant's name. Within **$10**, design a test that shows whether yours does."

| | |
|---|---|
| Method | Matched pairs: same facts, only the name changes. The correct flip rate is **0%**. |
| Deliverable | Your flip rate, plus one sentence on what you changed in the prompt to reduce it |
| What a good answer shows | A prompt that scores well can still be biased. Measurement validity is a separate question from accuracy |

---

### Estimation worksheet (all cases)

1. Maximum affordable cost per item = budget ÷ items: ______
2. Guess tokens in per item: ______  tokens out per item: ______
3. Model and price per million tokens (in / out): ______
4. Projected full-job cost: ______  → within budget? yes / no
5. After the sample run: actual projected cost ______  Error: ______ %
6. Lever that changed the most: ______
