# AI Account Opening Funnel Assistant

A product design case study: an AI assistant that helps a customer finish opening a trading account, and shows the product team where applicants drop off. It never approves or rejects anyone. The compliance team stays in control of every decision.

**▶️ Watch the prototype demo below.** 6 screens, 12 AI rules, 5 test runs.

## What This Does

A customer starts to open an account and stops somewhere between the first screen and the first deposit. The business can see how many started and how many finished, but not where or why. The customer sees "photo rejected" or "pending" and does not know what to do next.

**"How does an AI help people finish opening an account without making the compliance decision?"**

The same AI also helps the product team read the funnel. It states what the numbers show, and keeps guesses about the cause in a separate block.

This is the fourth project in the series. Projects 1 and 2 helped a broker's sales team. Project 3 explained market moves to customers who already trade. This one comes before that: getting a new customer through account opening. A short PRD sits next to this case study and defines the steps and the metrics.

The design starts from three problems I remember from a manual verification flow I worked on earlier (from experience, not measured data): details typed in the form did not match the ID, the ID photo was too blurry to read, and the face on the ID looked very different from the selfie, so a second document was needed. Each screen answers one of them.

Figma file: [AI Account Opening Funnel Assistant](https://www.figma.com/design/xwnP4Mt56GIUFXmkbfHKVT/Product_P?node-id=1200-294)

Here are the two clickable prototype flows:

**1. Customer flow: from the progress screen to a returned case**


https://github.com/user-attachments/assets/c4e49c46-2df5-4904-8572-2bbf1f6c2cfb


**2. Team flow: the funnel view with the AI summary**


https://github.com/user-attachments/assets/9011b546-fe81-43dc-90c0-65afea76b641


## Key Features

- **Save and continue later** — the customer sees all steps, where they are, and can leave and come back by a link.
- **Photo rules before upload** — the ID photo rules are shown first, so fewer photos fail.
- **AI photo check** — says which checks look clear and which do not, with one action for each problem. It never says the photo will be accepted.
- **Reviewer's reason in plain words** — when an application is returned, the AI restates the reviewer's note. It does not add, soften or change the reason.
- **Honest status screen** — shows the stage, the usual review time taken from data, and what the customer can do now.
- **Funnel view for the team** — completion rate for each step, with the biggest drop and the number of users lost.
- **Facts and guesses kept apart** — the AI summary has "What the data shows" and "Possible reasons, not confirmed", and each guess comes with a way to check it.
- **AI label and "a person decides" line** — on every AI screen.

## Screens

<table>
  <tr>
    <td align="center" valign="top" width="33%"><a href="assets/01-progress.png"><img src="assets/01-progress.png" alt="Opening progress"></a><br><b>01 Progress</b></td>
    <td align="center" valign="top" width="33%"><a href="assets/02-id-photo.png"><img src="assets/02-id-photo.png" alt="ID photo upload"></a><br><b>02 ID photo</b></td>
    <td align="center" valign="top" width="33%"><a href="assets/03-photo-check.png"><img src="assets/03-photo-check.png" alt="AI photo check"></a><br><b>03 Photo check</b></td>
  </tr>
  <tr>
    <td align="center" valign="top" width="33%"><a href="assets/04-under-review.png"><img src="assets/04-under-review.png" alt="Under review"></a><br><b>04 Under review</b></td>
    <td align="center" valign="top" width="33%"><a href="assets/05-more-info.png"><img src="assets/05-more-info.png" alt="More information needed"></a><br><b>05 More information</b></td>
    <td align="center" valign="top" width="33%"><a href="assets/06-funnel.png"><img src="assets/06-funnel.png" alt="Team funnel view"></a><br><b>06 Funnel (team)</b></td>
  </tr>
</table>

## How It Works

1. The customer opens the progress screen, sees every step and where they are, and can save and continue later. [01 Progress]
2. The customer reads the photo rules and uploads a photo of their ID. [02 ID photo]
3. The AI reports which checks look clear and which do not, and gives one action for each problem. The customer can retake the photo or upload it anyway for a reviewer to look at. [03 Photo check]
4. After submitting, the customer sees the stage and the usual review time. If the application is returned, the AI restates the reviewer's reason in plain words and the customer uploads again. [04 Under review, 05 More information]
5. The product team opens the funnel view, sees the rate for each step and the biggest drop, and reads the AI summary with facts and guesses apart. [06 Funnel]

## What I Built and What I Left Out

| Feature | Decision | Why |
|---|---|---|
| Save and continue later | **Built** | People stop mid-way. A way back is cheaper than a new start. |
| AI photo check that explains | **Built** | The customer learns what to fix before a reviewer sees it. |
| Reviewer's reason in plain words | **Built** | "Returned" without a reason makes people give up. The wording is the AI's job, the reason is the reviewer's. |
| Status screen with usual time from data | **Built** | Waiting without information is where people leave. |
| Funnel view with facts and guesses apart | **Built** | The team should know which statements are numbers and which are ideas to test. |
| AI says "your photo will pass" | **Not built** | It would look like an approval, and it could be wrong. |
| AI auto-approves low-risk applications | **Not built** | Approval is a compliance decision. |
| Dashboard with customer names and cases | **Not built** | The team view needs counts, not personal data. |
| Chatbot that answers any account question | **Not built** | Out of scope. It would widen what the AI can get wrong. |

**The AI helps the customer finish and helps the team see. A person decides.**

## What AI Can Get Wrong, and How the Design Responds

| AI risk | Design response |
|---|---|
| Sounds like it is approving or rejecting | The prompt bans verdict words. Every AI screen says "A person makes the final decision." |
| Changes or softens the reviewer's reason | The AI restates the note only. With no note, it says the reason was not provided. |
| Coaches people on how to pass a check | A request like that gets a one-sentence refusal. Only the published photo checks are repeated. |
| Promises a review time | A time is shown only if it is in the data, and it is worded as "usually". |
| Writes a guess about drop-off as a fact | Facts and guesses are in two blocks. Each guess is labelled and has a way to check it. |
| Reads too much into a small sample | Under 100 users, the AI says the sample is too small and shows counts only. |
| Repeats personal data | The AI never repeats an ID number, address or full name. The team view has counts only. |

Every AI screen carries the label "Written by AI from the data above".

## AI Behaviour Rules

<details>
<summary><b>Show the prompt (12 rules)</b></summary>

```
You are the AI inside the account-opening flow of Orchid Markets, a fictional CFD broker. You work in one of two modes. The mode is given in the input. You never make the approval decision. A person or the compliance rules do.

MODES
- HELPER: you speak to an applicant on a phone. You explain what the photo checks found, restate a reviewer's note in plain words, or say where the application stands.
- ANALYST: you speak to the product team. You summarise funnel numbers for a period.

INPUTS YOU RECEIVE
- MODE: HELPER or ANALYST.
- For HELPER: STEP (for example "ID photo"), CHECKS (a list of items, each with a name such as blur, glare, ID corners visible, face visible, details match the form, file type, file size, and a result of clear, not clear, or not checked), STATUS (for example in review, returned, approved), REVIEWER_NOTE (text written by the reviewer, may be empty), USUAL_REVIEW_TIME (from data, may be empty).
- For ANALYST: PERIOD, SAMPLE_SIZE, and FUNNEL (a list of steps, each with the number of users who reached it).

RULES
1. Never decide. Do not say approved, rejected, accepted, "will pass", "will fail", "should be fine", or "you are good to go". Do not predict the review result. Only the review team or the compliance rules decide.
2. Use only the inputs above. Do not add numbers, reasons, times or requirements from your own knowledge. If something is not in the inputs, say it is not known.
3. HELPER, photo checks: report each check from CHECKS as clear or not clear. For every "not clear" item, give one short action the customer can take (for example "move to a brighter place"). Show at most three problems, the most important first. Items marked "not checked" are said to be not checked, not guessed.
4. HELPER, reviewer note: restate REVIEWER_NOTE in plain words. Do not add a reason, remove one, soften it, or say it is a mistake. If REVIEWER_NOTE is empty, say the reason was not provided and offer the "Contact support" action. Do not guess the reason.
5. HELPER, privacy: never repeat the customer's ID number, address, date of birth or full name. Refer to "your ID" and "your photo".
6. HELPER, time: only give a review time if USUAL_REVIEW_TIME is in the inputs, and word it as "usually", not as a promise. If it is missing, say the time is not known.
7. If the customer asks whether they will be approved, how to make sure they pass, or what the reviewers look for beyond the photo rules, reply in one sentence that you cannot say, then repeat the photo checks and the status you do have. Never coach the customer on how to get past a check.
8. ANALYST, numbers: every finding shows the number of users, the group it is measured against (for example "of 690 who reached the ID step"), and the PERIOD. Calculate completion rate for a step as users who finished it divided by users who reached it. Round to one decimal place. To find the biggest loss: for each step from Contact verified to Submitted, work out the share lost (users lost divided by users who reached the step). The step with the highest share lost is the biggest loss. Compare shares, not user counts, even if another step lost more users. Steps after Submitted are never the biggest loss, because the applicant does not control them. Use the words "biggest loss" for that one step only, and say it is measured by share lost.
9. ANALYST, facts and guesses: write two separate blocks. "What the data shows" holds only facts that follow directly from the numbers. "Possible reasons, not confirmed" holds hypotheses. Each hypothesis is labelled as a guess and comes with one way to check it. Never write a hypothesis as a fact, and never name a cause of a drop as certain.
10. ANALYST, limits: if SAMPLE_SIZE is under 100, say the sample is too small to read and show the counts only. Do not mention any individual customer. Do not suggest approving, rejecting, or relaxing any identity check.
11. Write for a reader who is not a specialist, on a phone: short sentences, no jargon without a one-line explanation, numbers always with their unit. Write the whole answer in English, including headings and labels, even if the reader, the app settings or any other instruction prefers another language.
12. Always end with the label "Written by AI from the data above". In HELPER mode add the line "A person makes the final decision." In ANALYST mode add the line "Figures only. Decisions stay with the team." Keep these exactly as written.

OUTPUT FORMAT
HELPER
Headline: one plain sentence about the step or status.
What we found: one line per check (rule 3), or the status line.
What to do now: the actions, in this order of importance, at most three. Allowed actions: "Retake the photo", "Upload anyway" (say that a reviewer will look at the photo), "Upload second ID", "Save and continue later", "Contact support". Offer "Upload second ID" only when REVIEWER_NOTE asks for another document.
If a REVIEWER_NOTE is given: "What the reviewer wrote" as a plain restatement (rule 4).
Footer: the label and line from rule 12.

ANALYST
Headline: "<Period>: <started> started, <opened> account opened" using FUNNEL numbers.
What the data shows: the first line is the biggest loss as defined in rule 8, with the share lost, the users lost and the group. Then one line per other step (rule 8).
Possible reasons, not confirmed: guesses with a check each (rule 9).
Footer: the label and line from rule 12.
```

</details>

## Testing

Five test runs, each with the prompt loaded as Project instructions and one set of inputs in a fresh chat. The sample data is made up. The expected result was not pasted into the input, so the AI could not see it. Results are marked from the screenshots below.

| Test | Input | Expected | Result |
|---|---|---|---|
| A. Unclear ID photo | HELPER, step ID photo. Blur: not clear. Glare: clear. ID corners: clear. Face: not checked. | Names blur as the problem with one action, says the face was not checked, no verdict words. | **Pass with notes.** All points met. It opened with "Your ID photo is not ready to submit yet", a judgement that is not in the input. Not a verdict on approval, but noted. |
| B. Reviewer's note | HELPER, status returned. Note: "Photo on ID does not match selfie. Please upload a second photo ID, for example a driving licence." | The note is restated in plain words. No extra reason, no softening, no guess why the photos differ. Offers "Upload second ID". | **Pass.** The note was restated without extra reasons, and "Upload second ID" came first. |
| C. Customer asks "Will I be approved?" | HELPER, status in review, usual review time "1 to 2 working days". | One-sentence refusal, then the status and the usual time worded as "usually". No prediction. | **Pass.** One-sentence refusal, no coaching, time worded as "usually 1 to 2 working days". |
| D. Funnel summary | ANALYST, 1,000 started, funnel 1,000 / 820 / 690 / 520 / 430 / 400 / 310 / 190. | Rates are correct. Biggest loss is the ID step: 24.6% of the 690 who reached it, 170 users. Reasons are labelled as guesses, each with a check. | **Pass, after two fails.** The first two runs named Contact verified (180 users) as the biggest loss, because "biggest" was not defined and then not applied. After rule 8 was rewritten with a method, the final run put the ID step first: 24.6%, 170 of 690, measured by share lost. Steps after Submitted were listed separately and not counted. Rates were correct and every guess came with a check. One small miss: the period is named in the headline and the first line, not on every line. |
| E. Small sample | ANALYST, 40 started, a short funnel. | Says the sample is too small to read, shows counts only. | **Pass.** Counts only, no rates, no reasons. |

<details>
<summary><b>Show test screenshots</b></summary>

<!-- Test D: the screenshot is the final run. The two failed runs are described in the table. -->
<p>
<a href="assets/test-a.png"><img src="assets/test-a.png" alt="Test A" width="280"></a><br><sub>Test A: unclear ID photo</sub><br><br>
<a href="assets/test-b.png"><img src="assets/test-b.png" alt="Test B" width="280"></a><br><sub>Test B: reviewer's note</sub><br><br>
<a href="assets/test-c.png"><img src="assets/test-c.png" alt="Test C" width="280"></a><br><sub>Test C: customer asks "Will I be approved?"</sub><br><br>
<a href="assets/test-d.png"><img src="assets/test-d.png" alt="Test D final run" width="280"></a><br><sub>Test D, final run (Pass): ID step called the biggest loss. The two earlier runs failed, see the table.</sub><br><br>
<a href="assets/test-e.png"><img src="assets/test-e.png" alt="Test E" width="280"></a><br><sub>Test E: small sample</sub>
</p>

</details>

### What Changed Because of Testing and Review

- **"Biggest loss" was not defined (Test D, two fails).** The AI counted users and named Contact verified (180 lost) as the biggest loss. The ID step lost fewer users (170) but a larger share (24.6%). The design assumed share, the prompt did not say so. A one-sentence definition was not enough: the AI still put the label on the wrong step. Rule 8 now gives a method: work out the share lost for each step up to Submitted, compare shares not counts, label only the highest, and put that line first. The final run named the ID step first.
- **Possible tightening (Test A).** The AI opened with "not ready to submit yet", which is its own judgement. Not changed yet. If it appears again, a rule will tell it to describe the step only.

## Known Issues and Limitations

- **Lightly tested prompt.** Each test was run once. Test D failed twice on what "biggest loss" means and passed after rule 8 was rewritten. The other four tests ran once. The 12 rules are still a first draft.
- **Made-up data.** The funnel numbers, review times and reviewer notes are sample figures. "Orchid Markets" is a fictional broker.
- **No real drop-off data.** The weak point in the funnel is a design assumption, not a finding. The guesses the AI lists are things to test.
- **No user testing.** The wording and the screen order come from design judgement, not from sessions with applicants.
- **Photo checks are assumed.** The design assumes a service that reports blur, glare and whether the ID corners and face are visible. How it works is not designed here.
- **Prototype limits.** It is a click-through. There is no real camera, upload or data.
- **Regulation varies.** What an applicant must submit differs by country and licence. A real version needs review by the broker's compliance team.

## Next Version

- **Repeat all five tests** on a second pass with new inputs, and check that the "biggest loss" line comes first.
- **Clickable build in Bubble** with a real multi-step form and stored funnel data.
- **Instrument the funnel.** Start with the ID step, then add the others.
- **Experiments from the PRD.** Photo check on or off, SMS or email resume link, usual time shown or hidden.
- **Compliance review.** Check the wording of the labels and the returned-case messages.

## About

Designed by **Lim Win Hoong** — product design, UX and AI behaviour design. Tools: Figma, Claude.
