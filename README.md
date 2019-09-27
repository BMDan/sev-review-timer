# sev-review-timer
Tool to help coordinate and align attendees at SEV Review/Incident Review with timing requirements

# Installation
Download [the latest ZIP from master](https://github.com/lyft/sev-review-timer/archive/master.zip).  Stick it in a folder.  Open it in your favorite browser.

Alternatively, clone the repo.  Open "index.html".

# Usage
## Quickstart
Enter the number of SEVs and the End Time for the review.  Hit "Start".  As each SEV is completed, hit "Skip" or "Complete" (at the moment, they do the same thing).

## Interface
The three bars at the bottom represent the time assigned to the current SEV, the time assigned to SEV review as a whole, and the fraction of SEVs that have been completed.

## Timing Calculations
The time assigned to each SEV is equal to one-(# sevs remaining)th of the time remaining in SEV review (measured from when the current SEV started, not `now()`, so that it's stable).  This means that if you finish a SEV early, later SEVs will automatically have more time budgeted for their discussion.  Conversely, if you finish one late, remaining SEVs are compressed.

## The Extend button
Don't be confused by the "extend" button; its usage is purely optional.  It works by assigning some extra weight to the current SEV.  Essentially, each time you press it, you reduce the time allocated to the remaining SEVs.  If you don't use that time, it's "refunded" when you move on to the next SEV.  A few of us agreed that there's sometimes merit in running a SEV over its allotted time, but there's rarely benefit in running a SEV *well* over its allotted time.  This button serves to insulate against the bar being "stuck" at 100% and there otherwise being no apparent difference between overrunning by twenty seconds and overrunning by twenty minutes.

**Suggested usage**: be willing to hit "extend"—perhaps twice at most—if the discussion is going well.  Each time you do, say something like, "This discussion is going well, so I'm going to extend it by a bit, but we're borrowing time from the rest of the schedule and really need to wrap up before this hits 100%."

# Upgrades
I'm sure you can figure it out.

# Support
Self-service support is available at [this link](https://github.com/lyft/sev-review-timer/compare).  Or in the [#incident-managers channel on Slack](https://lyft.slack.com/archives/CNGJK8H1S).

# Known Bugs
* Except for JQuery and Bootstrap CSS, this script has no external dependencies or links.  It's probably worth inlining a copy of those two things so that it can be run entirely offline.  PRs welcomed.
* Though it incorporates timers, it should be sleep/resume/steal-safe.  It is not, however, clock-safe; if you change timezones in the middle of execution, the "end time" will get weird.  Everything else should work, however.
* SEV reviews that span calendar dates (in the execution context's current timezone) are not supported.  This is not assumed to be a very common or pressing issue.

# Important Notes and Disclaimers
I genuinely apologize to you if you choose to read the code.  Remember, nobody made you read it.  You chose to do that.

The timer is a tool, nothing more.  If you're using it as a process, you're doing it wrong.
