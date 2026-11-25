# ARIN121 Travel Planner

A system prompt for an AI travel planning assistant, developed in Google AI Studio Playground for ARIN 121 (Assignments 2 and 3).

## Purpose
The planner helps travellers organise a trip. It can plan a new trip from scratch or revise a plan the traveller already has. It is meant for people planning short leisure trips, for example students on a budget.

## Files
- `system-prompt.md`: the complete system prompt (current version). Earlier versions, including the Assignment 2 starting prompt, are in the commit history.
- `development-log.md`: the tests run on each version, what they showed, and the decision taken.

## How to use it
1. Open Google AI Studio Playground and paste the contents of `system-prompt.md` into System Instructions. Merging on GitHub does not update Playground, so copy the latest version by hand.
2. Start a new chat. If you ask for general help ("I'd like some help with a trip"), the planner shows a menu:
   1. **Plan a new trip**: it collects your trip details, confirms a summary with you, then builds a day-by-day itinerary with accommodation options and a budget check.
   2. **Revise an existing plan**: paste a plan (or use the one it just made) and say what to change. It proposes changes to the affected days only, re-checks the budget, and asks whether the result works before giving the final version.
3. Choose with a number, the activity name, or your own words. If your request is already clear ("revise my itinerary"), the activity starts directly.
4. You can switch activities at any time ("actually, help me fix my cousin's plan instead"). The destination, dates, travellers, budget and preferences you already gave are carried over.

## Features
- Activity menu with switching and carry-forward of trip details (new in Assignment 3)
- Plan revision: changes only the affected days, states what stays unchanged, recalculates the cost per person after each round, and finishes with the full revised itinerary and a "What changed" list (new in Assignment 3)
- Trip summary and confirmation before any itinerary
- Three accommodation options (low-cost, mid-range, higher-end) with cost per person
- Budget tracking with a Cost per Person table and cheaper alternatives when over budget
- Clarifying questions for ambiguous destinations (for example, which Kingston)
- Application boundaries: travel planning only

## Limits
- No live data: prices, opening hours and accessibility details are estimates from the model and must be checked before booking.
- No booking, maps or real-time availability.
- The menu offers two activities only.
- Each behaviour was tested with one conversation per test (Gemini 3.8 Flash), so results may vary between runs.
