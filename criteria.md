# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

**Overall accuracy ≥ 0.85 on the held-out test set.**

**Why this target:** `labels.csv` has 316 rows, and `analysis` is 69.3% of
them. An 0.85 accuracy target is 15.7 percentage points above simply predicting
that largest class, so it asks for useful overall performance rather than a
majority-label shortcut.

---

## 2.

**Per-label F1 ≥ 0.70 for every label with at least 20 test examples.**

**Why this target:** The held-out split has 33 `analysis` examples, 10
`hot_take` examples, and only 5 `reaction` examples. A 0.70 F1 floor guards
against ignoring a label while avoiding a brittle per-label threshold on tiny
supports; on this split only `analysis` reaches the 20-example condition.

---

## 3.

**Predicted label prevalence within ±10 percentage points of gold test-set
prevalence for each label.**

**Why this target:** The full dataset is already uneven (69.3% `analysis`,
19.9% `hot_take`, 10.8% `reaction`), so a model that predicts only the largest
label could otherwise look deceptively accurate. A 10-point tolerance checks
that predictions still reflect the smaller labels without demanding identical
shares on a 48-post test set.

---

## 4.

**Cohen’s κ ≥ 0.75 against human labels on the held-out sample.**

**Why this target:** With 215 of 316 rows marked as AI-suggested and still
unreviewed, accuracy against this file is not independent human agreement.
Kappa of 0.75 is a meaningful beyond-chance target only when evaluated against
an independently human-labeled sample; the current provisional labels cannot
establish that result.

---

## 5.

**Expected Calibration Error (ECE) ≤ 0.05, and predictions with confidence
≥ 0.80 must have empirical precision ≥ 0.75.**

**Why this target:** `analysis` is nearly seven times as common as `reaction`,
and their boundary depends on whether a specific fact supports an argument or
the post mainly expresses an immediate feeling. Calibration and the 0.80
confidence check make sure the model does not present those uncertain boundary
calls as reliable.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
