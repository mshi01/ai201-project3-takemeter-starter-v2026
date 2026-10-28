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
Community: r/tennis.

The classifier will sort the posts into 3 labels "reaction", "analysis" and "hot_take".


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `label_one`
analysis

**Definition:**

A post which makes an argument or explanation using specific, checkable evidence such as statistics, comparisons, or examples. An opinion supported by evidence.

**Example 1:**

She saved 8 of 10 break points and won 72% of points at the net. That combination made the close scoreline misleading because she controlled the important points.

**Example 2:**
>
Mertens serving 80% first serves and winning 77 points tells you everything, Iga never got a foothold in that one.

### `label_two`
hot_take

**Definition:**

A post is a hot_take when it makes a confident, broad, or provocative opinion without providing meaningful supporting evidence.

**Example 1:**

Clay-court tennis is the only surface that rewards actual skill

**Example 2:**
>
Such a ridiculous discussion. He's doing just fine against the top 10, besides Sincaraz which is pretty understandable.

### `label_three`
reaction

**Definition:**

A post is a reaction when it expresses an immediate response to something that just happened. It usually communicates an emotion, personal experience, or quick impression rather than developing an argument.

**Example 1:**
>
She played out of this world...Her best match of her whole career...

**Example 2:**
>
2 hours 54 minutes match and she's going to play a doubles match soon.


### The hardest boundary

**Which two labels:**

hot_take vs. reaction
analysis vs. hot_take

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
If the post mainly expresses an immediate feeling, it is a reaction. If it supports a claim with checkable evidence,it is analysis. Otherwise, if it makes a confident unsupported opinion,it is hot_take.


---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
r/tennis
**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
     Say so plainly — the disclosure is required, not penalised. -->
Cold first, followed by pre-labeled with AI and then checked each one.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| analysis | 67 | 33.3% |
| hot_take | 67 | 33.3% |
| reaction | 66 | 33.3% |
| **Total** | 200 | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
The besties be falling like dominoes in China. First Alex and now Zeynep.
> *Could have been:*
hot_take
> *I chose, because:*

reaction
Although with emotional wording, it is an immediate response to recent events.

**2.**
> *The post:*
There was a very long stretch in the first set where Bencic was barely winning points, which was wild to see.
> *Could have been:*
analysis
> *I chose, because:*

reaction
The statement of "which was wild to see" made it reasonable for a post to be a reaction. It did not explain why the stretch mattered, so reaction is more reasonable.

**3.**
> *The post:*
The funny thing is he will be missing out more money because of skipping 6 kings, than the money he would get from the bonus pool.
> *Could have been:*
analysis
> *I chose, because:*

hot_take
This post is more of expressing the opinion with emotions rather than analyzing the fact. 
---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**
"distilbert-base-uncased"
**Settings:** <!-- epochs, learning rate, batch size, seed -->
seed 42, 3 epochs, lr 2e-05, batch 16
**Anything I changed from the defaults, and why:**
N/A
**Split sizes:** <!-- train / val / test, and per-label counts in the test
     split. If a label had fewer than about 8 in test, say so — it explains a lot
     of next unit's variance. -->
70/15/15 (train/val/test)


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*

I asked what types of labels could be difficult to label?

- *What came back:*

It suggested that analysis and hot_take could be difficult to label as both might be expressing an opinion. 

- *What I changed:*

I think distinguishing analysis from hot_take is relatively easy because analysis is supported by evidence, while a hot take is not. However, distinguishing hot_take from reaction can be more difficult because both may use strong or emotional language. A hot take expresses a confident opinion, while a reaction expresses an immediate response to a recent event. 

**Moment 2**

- *What I asked for:*

I asked it to suggest another criterion to use to gauge the model performance and accuracy.

- *What came back:*

It suggested that on a second blind labeling of 30 randomly selected posts, the model must agree with my final labels on at least 21 posts, or 70% agreement.

- *What I changed:*

I replaced this criterion because it required a second blind labeling of randomly selected posts, which would have functioned as another test set. I chose a different criterion to avoid duplicating the test-set evaluation.

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
| Overall accuracy | 0.333 | 0.933 | +0.600 |
| Macro F1 | 0.167 | 0.933 | +0.766 |
| F1 — `analysis` | 0.500 | 0.909 | +0.409 |
| F1 — `hot_take` | 0.000 | 1.000 | +1.000 |
| F1 — `reaction` | 0.000 | 0.889 | +0.889 |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->
I predit the overall accuracy and F1 for each labels will be higher in trained vs baseline samples. 

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->
The trained model increased the overall accuracy and F1s for each label, which means the model has learned from training and thus the accuracies increases. 


---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >= 0.65 | 0.93 | 0.9 | 0.9 | MET |
| 2. Every label F1 | >= 0.60 | 0.93 | 0.9 | 0.9 | MET |
| 3. Test-set label distribution | 20% - 46% | 33% | 33% | 33% | MET |
| 4. Disagreements involve reaction versus hot_take | >= 75% | 0% | 66% | 33% | MISSED |
| 5. Among predictions with confidence of at least 0.80, must be correct on the held-out test set. | >= 75% | 100% | 90% | 100% | MET |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | analysis | hot_take | reaction |
|---|---|---|---|
| **analysis** | 10 | 0 | 0 |
| **hot_take** | 0 | 10 | 0 |
| **reaction** | 2 | 0 | 8 |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

Biggest confusion: 2 real `reaction` posts called `analysis`.
The other direction: 0 real `analysis` posts called `reaction`.

Roughly symmetric — the model finds this pair hard in both directions,
which more often means the boundary itself is genuinely hard.

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Overall accuracy | >= 0.65 | MET | For all 3 seeds, the overall accuracy was >= 0.65 |
| 2 | Every label F1 | >= 0.60 | MET | For all 3 seeds, every label F1 was >= 0.60 and F1 macro for each seed was >= 0.60 |
| 3 | Test-set label distribution | 20% - 46% | 33% | MET | For the 200 training samples, each label constitutes ~33%. During splitting, samples were stratified to have 1/3 of each label. Thus each label was ~33% in the test sets.
| 4 | Disagreements involve reaction versus hot_take | >= 75% | MISSED | Each disagreements involve involve reaction vs hot_take did not occupy >= 75% |
| 5 | Among predictions with confidence of at least 0.80, must be correct on the held-out test set. | >= 75% | MET | accuracy_most_confident_third >= 90% for each seed runs |

**Diagnoses**

For Criteria 4, for Seed=42, there are 2 reaction posts predicted as analysis; for Seed=7, there are 1 hot_take post predicted as reaction and 1 reaction post predicted as analysis and 1 reaction post predicted as hot_take; for Seed=2024, there are 1 analysis post predicted as hot_take, 1 hot_take post predicted as reaction, and 1 reaction post predicted as analysis. Each disagreements involve involve reaction vs hot_take did not occupy >= 75%. There are disagreements between other labels, such as reaction vs analysis and hot_take vs analysis.


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

**Agreement rate:** _30__ / 30 = _100__%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

As 30 out of 30 were agreed, this part was not provide.
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

<!-- **1.**
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

**What the pattern in my disagreements tells me:** -->



---

## The Improvement

**What I changed:**

Add more example posts to the "reaction" label in labels.csv. 

**Which diagnosis pointed at it:**

Since the biggest confusion from real "reaction" post predicted as "analysis". "reaction" is the thinnest label. I would like to add 30 more reaction posts for training set. 

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >= 0.65 | 0.91 | 0.86 | 0.89 | MET |
| 2. Every label F1 | >= 0.60 | 0.92 | 0.86 | 0.89 | MET |
| 3. Test-set label distribution | 20% - 46% | 29% | 29% | 42% | MET |
| 4. Disagreements involve reaction versus hot_take | >= 75% | 66% | 50% | 25% | MISSED |
| 5. Among predictions with confidence of at least 0.80, must be correct on the held-out test set. | >= 75% | 100% | 91% | 100% | MET |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->
The added reaction examples may have helped reaction recall slightly, but they did not improve overall test performance in this run.

For the missed criteria, criteria 4, it only slightly increased the number of disagreement post which involve reaction vs hot_take. 


---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

To measure the effect more rigorously, we can keep the original test set fixed and add the 30 posts only to the training portion.

**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->
I intended reaction to capture immediate emotional responses, while analysis should require a supported explanation or argument. The model still sometimes treats reactions that mention specific match details as analysis, suggesting it learned to rely on concrete tennis vocabulary more than on the difference between describing an event and explaining its significance.


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
