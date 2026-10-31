# PRD: AI Account Opening Funnel Assistant

Fictional broker: **Orchid Markets** (a made-up CFD broker in Malaysia). All figures are sample data in RM or counts. None come from a real company.

Owner: Lim Win Hoong. Status: draft for the portfolio case study.

## 1. Problem

A new customer who taps "Open account" has to pass several steps before they can trade: verify contact, fill in details, photograph an ID, take a selfie, wait for review, then make a first deposit. Many people stop part way. The business sees only "applications started" and "accounts opened", so it cannot tell where people stop or why. The customer sees "photo rejected" or "pending" and does not know what to do next.

Two questions for this case study:

1. **Customer side:** How can an AI help a customer finish the steps without making the compliance decision?
2. **Team side:** How can an AI explain where applicants drop off without inventing reasons?

### Where people got stuck in the old manual check (from my own experience, not measured data)

I worked on a similar manual verification flow two years ago. I do not have the numbers, only what I remember. These three cases were the most common:

1. Details typed in the form did not match the ID (for example a name spelled differently).
2. The ID photo was blurry or hard to read, so the reviewer asked the customer to send it again.
3. The face on the ID looked very different from the selfie, so the customer had to send a second document, such as a driving licence.

How the design answers them: the photo check reports "details match the form" as clear or not clear (case 1); the check flags blur and unreadable text before submit (case 2); the returned-case screen restates the reviewer's note and offers "Upload second ID" (case 3). The AI never decides any of these.

## 2. Goals and non-goals

Goals
- Raise the share of started applications that reach "account opened".
- Cut the number of ID photos that need a second try.
- Make "under review" and "more information needed" states clear enough that people come back.
- Give the product team one view of the funnel, with facts separated from guesses.

Non-goals
- The AI does not approve, reject or score applicants. A person or the compliance rules decide.
- The AI does not lower or skip identity checks.
- No personal data in the team dashboard. Counts and rates only.
- No fraud detection design in this version.

## 3. Users

| User | Need | What they should never get from the AI |
|---|---|---|
| Applicant (new customer, often on a phone) | Know what to fix, how long it takes, what happens next | A promise of approval, or a guess about the review result |
| Compliance reviewer | Fewer unreadable photos, clear returned-case notes | An AI recommendation to approve or reject |
| Product team | See where people drop and what to test | A reason stated as fact when it is only a guess |

## 4. Funnel definition

Count users once per step. A user who goes back is not counted twice.

| # | Step | Counts when | Owner of the outcome |
|---|---|---|---|
| S0 | Started | Customer taps "Open account" | Customer |
| S1 | Contact verified | One-time code accepted | System |
| S2 | Details done | Personal details form submitted | Customer |
| S3 | ID uploaded | ID photo passes the file check (format, size) | Customer |
| S4 | Selfie and declaration done | Selfie and signed declaration uploaded | Customer |
| S5 | Submitted | Application sent to review | Customer |
| S6 | Account opened | Reviewer or rules approve | Reviewer |
| S7 | First deposit | First deposit received, within 7 days of S6 | Customer |

Statuses after S5: Approved, Returned for more information, Rejected, Still waiting.

## 5. Metrics

| Metric | Definition | Why |
|---|---|---|
| **Account-open rate (primary)** | S6 / S0, within 14 days of S0 | The headline result |
| Step completion rate | Users finishing step N / users reaching step N | Finds the weakest step |
| Photo retry rate | Users who upload the ID more than once / users reaching S3 | Measures the AI photo check |
| Return rate | Returned for more information / S5 | Quality of what customers submit |
| Median time to approval | S5 to S6, in hours | Wait the customer feels |
| Resume rate | Users who leave and come back within 72 hours / users who leave | Measures save-and-continue and status screens |
| First-deposit rate | S7 / S6 | What happens after opening |

Guardrail metrics (must not get worse):
- Rejection rate and return rate. If the AI "helps" people through by hiding problems, these rise.
- Reviewer re-check time per case.
- Complaints that mention "AI said" or "AI promised".

Illustrative targets (design targets for the case study, not claims): account-open rate from 31% to 36% in the test group; photo retry rate down by a quarter.

## 6. Requirements

### Customer side
- C1. Progress screen shows all steps, where the customer is, and a "Save and continue later" action. Resume link by SMS or email.
- C2. ID upload shows the photo rules before the camera opens.
- C3. After each upload an AI pre-check reports what it could see (clear or not clear) and what to fix. It never says the photo will be accepted.
- C4. "Under review" shows the stage, the time the team usually takes (from data, not a promise), and what the customer can do now.
- C5. "More information needed" shows the reviewer's reason in plain words. The AI rewrites the wording only. It does not change, add or soften the reason.
- C6. Every AI text carries the label "Written by AI" and the line "A person makes the final decision."

### Team side
- T1. Funnel view: counts and rates for S0 to S7 for a chosen period.
- T2. Biggest drop is highlighted with the number of users lost and the base used.
- T3. AI summary has two parts: "What the data shows" (facts from the numbers) and "Possible reasons, not confirmed" (each with a way to check).
- T4. No personal data. No case-level view.
- T5. If the sample is under 100 users, the summary says the sample is too small to read.

### AI behaviour
See `prompt.txt`: one prompt with two modes (HELPER for customers, ANALYST for the team).

## 7. Sample data (fictional)

1,000 applications started in one 14-day period.

| Step | Users | Completion from previous step |
|---|---|---|
| S0 Started | 1,000 | — |
| S1 Contact verified | 820 | 82.0% |
| S2 Details done | 690 | 84.1% |
| S3 ID uploaded | 520 | 75.4% |
| S4 Selfie and declaration | 430 | 82.7% |
| S5 Submitted | 400 | 93.0% |
| S6 Account opened | 310 | 77.5% |
| S7 First deposit | 190 | 61.3% |

Account-open rate: 310 / 1,000 = 31.0%.
After submit (400): 310 approved, 70 returned for more information (17.5%), 20 still waiting.
Biggest drop: S2 to S3, 170 users lost (24.6% of those who reached the ID step).

I do not have real drop-off figures from my earlier work. The numbers above are made up so the screens and the AI summary have something to show. The reasons the AI may list for the S2 to S3 drop are hypotheses to test, not findings.

## 8. Risks

| Risk | Response |
|---|---|
| AI reads as approving or rejecting | Prompt bans verdict words. Label and "a person decides" line on every AI screen. |
| AI explains a returned case wrongly | AI only restates the reviewer's note. No note, no explanation. |
| AI coaches people on how to pass checks | One-sentence refusal. Only the published photo rules are repeated. |
| Dashboard invents a cause | Facts and hypotheses are in separate blocks. Each hypothesis has a check. |
| Personal data leaks into AI text | Counts only on the team side. The AI never repeats ID number, address or full name. |
| Rules differ by country and licence | A real version needs review by the broker's compliance team. |

## 9. What to test after launch (ideas)

1. Photo pre-check on or off: compare photo retry rate and return rate.
2. Resume link by SMS or by email: compare resume rate.
3. Show the usual review time or hide it: compare the number of "where is my application" contacts.

## 10. Open questions

- Which step to measure first if only one can be instrumented?
- Is the usual review time shown as a range or a median?
- Who owns the wording of returned-case notes: compliance or product?

## Appendix: the 6 screens

| # | Screen | Side | Purpose |
|---|---|---|---|
| 01 | Progress | Customer | See the steps, save and continue later |
| 02 | ID photo | Customer | Rules and an example photo before upload, upload area |
| 03 | Photo check | Customer | AI says what it saw and what to fix |
| 04 | Under review | Customer | Stage, usual time, what to do now |
| 05 | More information needed | Customer | Reviewer's reason in plain words, upload again |
| 06 | Funnel | Team | Biggest drop card, a card per step, AI summary with facts and hypotheses, back to home |
