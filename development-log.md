# Development log

Model and settings for every test: Gemini 3.8 Flash in Google AI Studio Playground, Thinking level Medium, all other settings default, all tools off (including Grounding with Google Search). Fresh conversation for each test.

## Version 1: Assignment 2 starting prompt
Commit: "Preserve Assignment 2 starting prompt". Features: trip summary and confirmation, accommodation options, budget tracking, clarifying ambiguous destinations, application boundaries. Tested in Assignment 2.

## Version 2: activity menu and plan revision activity
Commits: "Add an activity menu for planning and revising trips", "Add a plan revision activity that keeps unchanged days".

**Issue.** The planner could only build a new itinerary. In Assignment 2 we also saw Layla change days we had asked it to keep and let the budget rise while "fixing" a plan, so revising an existing plan is a useful activity to add, with clear limits on what it may change.

**Revision.** Added an Activity Menu module (menu text, selection by number, name or own words, switching with carry-forward of trip details) and a Plan Revision module (needed information, one question when information is missing, changes to affected days only, updated Cost per Person, confirmation question, completion with the full itinerary and a "What changed" list). Added three lines to existing modules so they do not conflict: the trip summary step applies to new trips only, accommodation is only re-suggested when the change concerns where to stay, and the boundaries include revising plans.

### Test 1: select and complete the new activity
- "I'd like some help with a trip." The menu appeared exactly as written.
- "2". It asked, in one message, for the plan and what to change.
- Pasted a 3-day Quebec City plan (2 students, CAD 500 each) and asked for less walking on Day 2. It replaced only Day 2 items, said "Day 1 and Day 3 stay exactly as you planned them", and showed an updated Cost per Person (CAD 393, within budget).
- "Better, but please keep the Citadelle." It changed only the Day 2 morning back (Citadelle reached by a short taxi ride), kept the rest, and recalculated (CAD 404). The totals add up.
- "Perfect." It gave the full revised itinerary once, a "What changed" list and the final cost, then ended.

**Observed result.** Behaved as specified. Limits: some details are the model's own and unverified (a student price, accessibility at the Citadelle), and the final version reworded Days 1 and 3 slightly while keeping the same activities and prices.

### Test 2: switch activities
- Started Plan a new trip: Montreal, 4 days in mid-March, 3 friends, CAD 450 each, food markets and museums. The planner showed the trip summary.
- Before confirming: "Actually, wait. My cousin already made us a plan for this trip, so could you help me fix that one instead? Mainly it feels too expensive."
- It confirmed the switch in one sentence, restated 3 travellers, 4 days, Montreal and CAD 450, and asked only for the plan.
- After the plan was pasted (without repeating the details), it compared it with the CAD 450 budget (CAD 1,021 per person, correct), kept the focus on museums and food markets, changed only the expensive items, listed the unchanged items, and reached CAD 447 per person.

**Observed result.** Switched and kept every established detail. Limit: it added a metro pass that was not in the original plan.

**Decision.** Keep version 2. No behavioural problem against the requirements, so no revision was made. Future improvement: tell the revision activity not to add new cost items unless the traveller asks.
