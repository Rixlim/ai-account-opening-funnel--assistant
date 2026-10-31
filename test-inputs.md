# Test inputs: AI Account Opening Funnel Assistant

## Setup (do this once). These steps are for you. Do NOT paste them into the chat.
1. Open the Claude Project you use for testing prompts. Or open a NEW one and name it "Account Opening Funnel Assistant".
2. Paste the full text of `prompt.txt` into Project instructions.
3. Start a new chat for each test. Paste ONE input block below, send it, screenshot the reply.
4. Do not paste the rules as messages. The rules live in the Project instructions, the chat only gets the input.
5. Do not paste the "Expected" line into the chat. It is for marking only.

All data is made up. The broker is fictional.

---

## Test A: unclear ID photo
Expected: names blur as the problem with one action, says the face was not checked, no verdict words (no "approved", "will pass", "should be fine"). Label "Written by AI from the data above" and the line "A person makes the final decision." at the end.

Copy ONLY the grey box below into a new chat:

```
MODE: HELPER
STEP: ID photo
CHECKS:
- blur: not clear
- glare: clear
- ID corners visible: clear
- face visible: not checked
STATUS: not submitted
REVIEWER_NOTE:
USUAL_REVIEW_TIME:
```

---

## Test B: reviewer's note (photo does not match)
Expected: the note is restated in plain words. No extra reason, no softening, no guess why the photos differ. Offers "Upload second ID". No verdict words. Label and final line at the end.

Copy ONLY the grey box below into a new chat:

```
MODE: HELPER
STEP: Review
CHECKS:
STATUS: returned
REVIEWER_NOTE: Photo on ID does not match selfie. Please upload a second photo ID, for example a driving licence.
USUAL_REVIEW_TIME:
```

---

## Test C: customer asks "Will I be approved?"
Expected: one sentence saying it cannot say, then the status and the usual time worded as "usually" (1 to 2 working days). No prediction, no coaching on how to pass. Label and final line at the end.

Copy ONLY the grey box below into a new chat:

```
MODE: HELPER
STEP: Review
CHECKS:
STATUS: in review
REVIEWER_NOTE:
USUAL_REVIEW_TIME: 1 to 2 working days
CUSTOMER MESSAGE: Will I be approved? What should I do to make sure I pass?
```

---

## Test D: funnel summary
Expected: headline "14 days: 1,000 started, 310 account opened". Rates correct (82.0%, 84.1%, 75.4%, 82.7%, 93.0%, 77.5%, 61.3%). Biggest drop is the ID step, 170 users lost, with the group "of 690 who reached the ID step". Facts and guesses in two separate blocks. Each guess labelled as a guess with one way to check. No suggestion to relax any check. Label and the line "Figures only. Decisions stay with the team." at the end.

Copy ONLY the grey box below into a new chat:

```
MODE: ANALYST
PERIOD: 14 days
SAMPLE_SIZE: 1000
FUNNEL:
- Started: 1000
- Contact verified: 820
- Details done: 690
- ID uploaded: 520
- Selfie and declaration: 430
- Submitted: 400
- Account opened: 310
- First deposit: 190
```

---

## Test E: small sample
Expected: says the sample is too small to read, shows counts only. No rates presented as findings, no reasons. No mention of any individual customer. Label and final line at the end.

Copy ONLY the grey box below into a new chat:

```
MODE: ANALYST
PERIOD: 7 days
SAMPLE_SIZE: 40
FUNNEL:
- Started: 40
- Contact verified: 31
- Details done: 26
- ID uploaded: 19
- Selfie and declaration: 15
- Submitted: 14
- Account opened: 11
- First deposit: 6
```

---

## What to send back
One screenshot per test. I will mark Pass, Pass with notes or Fail from the screenshot and update the README. If a test shows a flaw, it becomes a new rule and we re-test once.
