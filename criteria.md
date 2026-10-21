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

<!-- Your criterion. It must name a number. -->

The classifier must reach an overall accuracy of at least 0.65 on the held-out test set across all three random seeds.



**Why this target:**

There are three labels, so a roughly even random guess would be about 0.33 accuracy. A 0.65 target requires the classifier to identify the writing purpose substantially better than chance while allowing for ambiguity between `reaction` and `hot_take`.



---

## 2.

<!-- Your criterion. -->

The held-out test-set F1 score must be at least 0.60 for each label: `analysis`, `reaction`, and `hot_take`, across all three random seeds.



**Why this target:**

The labels have nearly equal counts, so the model should not be able to meet the project goal by ignoring one class. The lower per-label threshold reflects the difficulty of separating short emotional reactions from confident unsupported opinions.



---

## 3.

<!-- Your criterion. -->

The predicted test-set label distribution must keep every label between 20% and 46% of predictions for every random seed.



**Why this target:**

The training data is balanced at 67 `analysis`, 67 `reaction`, and 66 `hot_take` posts. A model that predicts one label for almost everything would have poor practical value even if its overall accuracy looked acceptable, so this range checks for severe collapse into one class.



---

## 4.

<!-- Your criterion. -->

On a second blind labeling of 30 randomly selected posts, the model must agree with my final labels on at least 21 posts, or 70% agreement.



**Why this target:**

The hardest boundary in this taxonomy is `reaction` versus `hot_take`, because both can use strong emotional language. Reaching 70% agreement on a fresh sample would show that the decision rules are specific enough to apply consistently rather than only fitting the original examples.



---

## 5.

<!-- Your criterion. -->

Among predictions with confidence of at least 0.80, at least 75% must be correct on the held-out test set.



**Why this target:**

The classifier will be more useful if its strongest predictions are usually trustworthy. A 0.80 confidence threshold leaves room for a small test set and for naturally ambiguous tennis posts, while 75% accuracy still requires confidence to carry meaningful information.



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
