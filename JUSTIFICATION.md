# JUSTIFICATION — the design of the harness, and why
Author: Subbotina Tanya

### Initial expectation

I wrote this after starting the legal search. I expected logging
to be the hardest control to link to a specific law, because the law
may require accountability without specifying exactly what our log
should contain.

## 1. What the system may do

The system may suggest applicants for a scholarship shortlist, but it does not award funding.
Names and universities are hidden. Grades, exam scores, income and achievements remain visible.
All model rejections and scores in the 40–45 band go to human review.

These settings are in HARNESS and BLIND. My additional rules are in my_extra_refusal
and my_extra_escalation. The notebook records referrals but does not run a real review service.

## 2. What it must refuse

The harness refuses the wrong purpose, applicants under 18, missing consent, invalid values
and certain instructions in text fields. It refused 5 of 6 test requests without model calls.
None of the 400 clean applicants would have been refused.

These rules have costs. Qualified minors are excluded from this prototype, and the keyword filter
could block harmless text. A manual application route is needed but is not implemented.
Refusals are logged, but applicants are not automatically notified.

## 3. What record it keeps

The log should explain what happened to an application and which controls acted.
It stores IDs, an input hash, model and prompt versions, settings, field names, raw output,
score, outcome, reason and timestamp. One record shows a rejection with score 20 being
sent to a person under rejection_needs_human_review.

There are 412 records because the six-request test ran twice after the main measurement.
The hash cannot reconstruct the input, and raw replies may repeat applicant information.
The log is editable and has no enforced access or deletion policy. These need to be added
before real use, together with records of the human review.

## 4. The legal constraints


I wrote my initial expectation after starting the search: logging seemed hardest to link
to a specific law because the law may not prescribe our exact record format.

I assume a future deployment in Kazakhstan. The current applicants are synthetic.
I use the following law as a design benchmark, not proof of full compliance:

[Law No. 94-V of 21 May 2013, On Personal Data and Their Protection](https://adilet.zan.kz/rus/docs/Z1300000094).

Article 7(1) addresses consent, with exceptions, and Article 19-1(1) addresses automated
processing affecting rights and legitimate interests. These support the consent check.
Article 7(8) and Article 14 support keeping processing within its stated purpose.

Article 12(1) supports collecting necessary and sufficient data. Blinding is our design choice.
Article 24(1)(2) concerns corrections: validation supports data quality but does not verify truth.
Article 24(1)(1) concerns information about processing: the log helps, but JSONL is not required.

Article 19-1(2)-(3) addresses explanations, objections and their consideration within three
working days. Referral supports oversight but does not implement the full objection process.
The age restriction, keyword filter and review band are additional design choices.
A real deployment needs further legal review.

## 5. The ethical principles

I use the [OECD AI Recommendation](https://legalinstruments.oecd.org/api/print?ids=648&lang=en),
adopted in 2019 and updated in 2024. It is non-binding guidance, not a Kazakhstan law.

Principle 1.2, fairness and privacy, supports blinding. Principle 1.4, robustness, security
and safety, supports validation and refusal checks. Principle 1.5, accountability, supports
logging. Principle 1.3, transparency and explainability, supports understandable decisions
and challenges, although referral alone is not enough.

There are conflicts: hiding details removes context, while logging creates privacy risks.
I chose limited model inputs and records that make investigation possible.

## 6. The trade-offs


Zero flips after blinding were expected because paired inputs became identical.
This does not prove fairness. Outcomes changed for 63/400 profiles and scores for 166/400.

I chose 40–45 because rejection and shortlist scores overlapped at 45 and the rejection
median was 40. The band covered 16.0% of baseline profiles. With all rules, the actual
review share was 14.5%. I kept the band after checking this workload, but did not validate
it on new data. Both runs used 400 model calls; human review is the main added cost.

Shortlists outside the band can still be wrong. One explanation treated consent as a reason
for shortlisting, although it should only allow processing. This needs further testing.
The system also still needs a real review queue, appeals, notifications and secure logging.

## AI-use declaration

I wrote the explanations and supporting documents myself. I used an OpenAI assistant to improve my
wording and grammar and make the English read more naturally. It also flagged possible inaccuracies in my explanations and suggested corrections,
which I reviewed and made myself. The assistant and me were thinking about additional refusal and referral rules, and I wrote the explanations for those rules.

I ran the notebook in Colab, and the reported figures come from my own run. The assistant helped me locate and check relevant
legal provisions. My references cite the original law and the OECD recommendation.

I still need to personally verify some of the cited provisions before submission. Features such as
appeals and secure log storage are listed as future work.
