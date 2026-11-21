# REPORT — what the measurement showed, who it affects, and whose responsibility it is
Author: Subbotina Tanya

## 1. Measurement read-out

For 40 pairs per attribute, language had 2 flips (5.0% [1.4%, 16.5%]), gender had
4 (10.0% [4.0%, 23.1%]), and university had 1 (2.5% [0.4%, 12.9%]).
The name floor was 0/40 [0.0%, 8.8%]; the university floor was 1/40 [0.4%, 12.9%].
No attribute clearly exceeded its floor.

All four gender flips favoured female-coded names, but p = 0.125. My prediction about
Kazakh names doing worse was not supported. Mean absolute score differences were
3.12 [1.38, 5.25] for language, 1.12 [0.25, 2.13] for gender, and 2.50 [1.12, 4.12]
for university. The floors were 2.00 [0.62, 3.62] and 2.12 [0.88, 3.62].
The signed flagship score advantage was +2.5 [+1.1, +4.1], but university flips matched
the floor. The other signed gaps were +0.7 for Kazakh names, +0.2 for Russian names,
-1.0 for English names, and -0.4 for male-coded names; their intervals included zero.

The exact test needs at least 6 one-directional flips with none in the other direction.
Smaller effects could remain undetected. The floors cover only the tested irrelevant
changes, so this run does not prove fairness or predict results for real applicants.

After blinding, all flips were zero because paired inputs became identical.
Outcomes changed for 63/400 profiles, and scores for 166/400. Prompt formatting also
changed, so these changes cannot be attributed only to the removed information.
Human review covered 58/400 (14.5%), against the baseline band's estimate of 16.0%.
Both runs used 400 model calls. The main added cost is reviewer workload.

## 2. Who is affected

Applicants could lose funding through an unfair rejection, while an undeserved shortlist
could displace someone else. The observed gender flips favoured female-coded names,
and the university flip favoured the flagship institution. Without ground-truth labels,
I cannot say which individual decisions were wrong.

Human referrals create delays and work for staff, and reviewers can also be biased.
The refusal rules blocked 5/6 test requests and 0/400 clean applicants, but the keyword
filter could still block harmless text. Applicants need a correction or manual route.
Repeated use could carry an initial mistake into later selection stages.

## 3. Professional responsibility

I implemented and tested validation, blinding, refusals, logging and human referral.
The log has 412 records because the six-request test was run twice after the main run.

One explanation treated consent as a reason for shortlisting. Consent should allow
processing, not improve merit, so this needs further testing. The prototype also lacks
an actual review queue, appeals, enforced retention and access rules, and tamper-proof logs.

The fund must define eligibility, provide reviewers and handle complaints. My responsibility
is to explain these gaps and avoid claiming that this synthetic test proves deployment
readiness. If controls are removed to save resources, I should document the resulting risks.
