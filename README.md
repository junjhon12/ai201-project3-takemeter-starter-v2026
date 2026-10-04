# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

I chose public Hacker News (news.ycombinator.com), using comments as the text to classify. I read 36 top-level comments across 13 discussions in the public Top Stories feed, spanning software, technology, games, and work. The comments ranged from brief reactions to detailed arguments and personal accounts. I will classify how comments support and develop a point, not whether I agree with them; these initial observations will guide, but do not settle, the labels for a 200-comment dataset.

### Candidate distinctions from the initial reading

- **Specific support:** Some comments include checkable details, links, numbers, or firsthand experience; others make a claim without an example. This appeared in the [browser-platform discussion](https://news.ycombinator.com/item?id=49950554) and [electrician discussion](https://news.ycombinator.com/item?id=49910462).
- **Explained reasoning:** Some comments connect evidence to a conclusion or compare alternatives; others offer a broad judgment without explaining it. For example, comments in the [RuneScape discussion](https://news.ycombinator.com/item?id=49949588) varied between a blanket assessment and a question grounded in player-count comparisons.
- **Qualification:** Some comments acknowledge uncertainty, tradeoffs, or another perspective while making their point. The [budget-caps discussion](https://news.ycombinator.com/item?id=49949235) included accounts of both the benefits and costs of hard limits.
- **Actionable detail:** Some comments identify a specific problem and suggest a change, while others are brief reactions. This contrast was visible in the [game discussion](https://news.ycombinator.com/item?id=49946393), from a short expression of enjoyment to detailed usability feedback.

This was a convenience sample of comments on current Top Stories, not a representative sample of all Hacker News comments. I will revisit these candidate distinctions while collecting and labeling the larger dataset.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** Makes a claim and supports it with a specific, checkable fact or example that does real work in the reasoning.

**Example 1:** “Is graphical fidelity what people are looking for in a RuneScape game? Unreal seems like an interesting choice. OSRS has something like 5x the player base and the gap only seems to be growing, so it looks odd to me to putting so much investment into a continuation of RS3.” ([comment](https://news.ycombinator.com/item?id=49950249))

**Example 2:** “Take for instance something like suggestions on form fields: you start typing something and it presents some options from a hardcoded list that matches the prefix. This is natively achieved through the HTML element `<datalist>`. However, `<datalist>` implementations on most browsers suck to the point of being unusable.” ([comment](https://news.ycombinator.com/item?id=49952769))

### `hot_take`

**Definition:** States a confident general judgment or prediction without offering specific evidence or reasoning to support it.

**Example 1:** “Everything Jagex touches turns to shit. They are not good at creating. At best they are a steward for already created IP and the community provides that taste that makes it good.” ([comment](https://news.ycombinator.com/item?id=49950936))

**Example 2:** “This is the year of old browser (and/or flash) games making a comeback in some form.” ([comment](https://news.ycombinator.com/item?id=49946711))

### `reaction`

**Definition:** Primarily expresses the writer's immediate personal feeling or experience in response to the linked item, without developing a broader argument.

**Example 1:** “This is a lot of fun (only tried on desktop)” ([comment](https://news.ycombinator.com/item?id=49953133))

**Example 2:** “Well, this is strangely familiar to a game I just vibe-coded recently!” ([comment](https://news.ycombinator.com/item?id=49948822))

### The hardest boundary

**Which two labels:** `analysis` and `hot_take`

**The decision rule I used every time:** If a specific, checkable fact or example materially supports the comment's conclusion, label it `analysis`, even if the tone is opinionated; if the opinion would stand unchanged without that detail, label it `hot_take`. A number or example that is merely decorative does not count as support.

### AI boundary stress test

These eight synthetic comments were generated to test the definitions; they are not dataset examples.

| Synthetic comment | Label | Why |
|---|---|---|
| “Across five cold starts, the page averaged 2.4 seconds to load, versus 0.6 seconds with the cache warm; uncached assets look like the bottleneck.” | `analysis` | The measured comparison supports the proposed cause. |
| “I tested the native date picker in Safari and Firefox; only Safari let keyboard users reach the month selector, so the API behavior is inconsistent.” | `analysis` | A specific, checkable test supports the conclusion. |
| “Native browser APIs are always a worse choice than libraries.” | `hot_take` | It is a broad, unsupported generalization. |
| “No one needs another task-management app.” | `hot_take` | It makes a sweeping judgment without support. |
| “Just opened the demo and I'm delighted; that little animation made my morning.” | `reaction` | The main point is an immediate personal feeling. |
| “I saw the announcement a minute ago and I'm honestly gutted; I was hoping they'd keep the old version.” | `reaction` | It reports a personal reaction to the announcement, not a broader argument. |
| “Support tickets about navigation rose from 20 to 36 the week the redesign shipped; that makes me think the new menu caused avoidable confusion.” | `analysis` | The concrete before-and-after count is offered as evidence for the conclusion. |
| “I just saw the new release. I hate this direction; the whole product is doomed.” | `hot_take` | The immediate feeling is present, but the comment's main claim is a broad unsupported prediction. |



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

**Counts per label:**

| Label | Count | Share |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**2.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**3.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
