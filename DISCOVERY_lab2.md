## Part 2: Assumption cards
“Assumption cards” are just a structured way to capture claims the team is relying on but has not yet verified. 

Use this format for each card:
- Assumption: We believe [stakeholder] currently does or needs [claim].
- Consequence: If this is wrong, [effect on value, scope, or feasibility].
- Evidence needed: What would confirm or challenge it?
- Question: What should we ask the stakeholder?
- Risk rank: 1–5, where 1 is the riskiest.

Example:
- Assumption: We believe support agents lose substantial time manually categorizing incoming tickets.
- Consequence: If this is wrong, automated categorization may provide little value.
- Evidence needed: Current triage workflow and examples of delays or errors.
- Question: Walk us through what happens from the moment a new ticket arrives.
- Risk rank: 1.

Create one assumption in each readiness area:
1. Problem and users
2. Evidence that the problem matters
3. Feasible independent MVP
4. Data/API/system access and fallback
5. Technical and verification approach

What is due today?
- A draft DISCOVERY.md on a branch or in a pull request.
- Five ranked assumptions.
- Five discovery questions linked to those assumptions.
- Discovery-labeled GitHub issues.
- The sibling team’s challenge.
- One recorded Keep, Stop, or Try action.
- Evidence of each member’s visible contribution for the possible individual studio check.

## Part 4: Issues to GitHub
See: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates

### Tracked discovery work

Create one GitHub issue for each unresolved question, evidence need, or follow-up. Use an action-oriented title such as:

- Investigate how referral coordinators identify overdue referrals
- Confirm what information is required before submitting a referral
- Ask how patients currently learn a referral’s status
- Verify a fallback when an external system is unavailable

For each issue, copy and complete this structure:

#### What we need to learn or do

[State one specific question, evidence need, or follow-up.]

#### Linked assumption

[Assumption ID and short description.]

#### Why it matters

[What decision about scope, priority, feasibility, or safety could change?]

#### Evidence or answer needed

[What would be sufficient to resolve this issue?]

#### Owner and next step

@[username] will [specific next action].

#### Done when

[Observable condition for closing the issue.] 

Index:
| Assumption | GitHub issue | Owner | Status |
|---|---|---|---|
| A1 | #__ | @username | Open |
| A2 | #__ | @username | Open |


### Example cycle:
1. Start with an assumption.
2. Identify the unresolved question.
3. Create the issue.
4. Apply the discovery label.
5. Assign an owner.
6. Add it to the board’s Backlog.
7. Link the issue number from DISCOVERY.md.

Avoid issue titles such as “Question 1,” “Research,” or “Do discovery”;

## Part 5: Sibling review
The workflow should be:
1. Each team opens its own DISCOVERY.md draft and gives the two-minute briefing.
2. The assigned sibling team listens and gives one advisory challenge.
3. The receiving team records that challenge in its own DISCOVERY.md or links a GitHub issue created from it.
4. The receiving team decides whether to act on the feedback.

Add a Sibling review to markdown:
```
## Sibling review
- Reviewer team:
- Challenge received:
- Assumption, stakeholder, or dependency affected:
- Team response: Adopt / Investigate / Decline
- Resulting change or GitHub issue:
```

Then, right below it:
```
## Team retro
- Keep:
- Stop:
- Try:
- Action for the next lab:
```
