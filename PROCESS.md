HOW THIS WAS BUILT

This project was built entirely through conversation with Claude, an AI assistant made by Anthropic. No code was written by hand. This document covers how that process worked -- the prompting approach, what landed well, what needed fixing, and how the tool evolved through iteration.


THE STARTING POINT

The first prompt wasn't technical at all. It was:

    "if i am working with a group of 15 people, what is the easiest thing to build in code in order to help us stay organized"

Claude asked a follow-up question to narrow down the problem: what's the biggest pain point -- task tracking, scheduling, announcements, or voting? The answer was deadlines, and from that single word, Claude proposed a deadline tracker and built a working interactive prototype directly in the chat.

That first version had the core structure: task cards, status badges, a stats bar, and filters. It was functional immediately.


PROMPTING TECHNIQUES THAT WORKED

Starting with the problem, not the solution

The opening prompt didn't say "build me a task tracker." It described a situation -- 15 people, staying organized -- and let Claude figure out what to build. This produced a more considered recommendation than jumping straight to a spec would have.

One change at a time (mostly)

The most reliable results came from focused prompts. "Add a delete button" produced a clean, well-integrated result. Trying to do everything at once came later, and it mostly worked -- but focused prompts were easier to verify and correct.

Describing behavior, not implementation

Prompts like "make the delete button pop up instead of just a red circle" and "show it when you hover over any part of the task, not just the right side" described what the experience should feel like rather than specifying CSS properties. Claude translated intent into implementation.

Asking for the file alongside the explanation

Requesting both the code file and the git steps in the same prompt ("give me the code for this and also the steps to put this into git") produced a complete package rather than a response that had to be followed up on.


WHAT WORKED WELL

Incremental feature additions held together

Each new feature -- dropdown assignees, delete button, time field, "All" option -- was added on top of the existing code without breaking anything. The file stayed coherent across many rounds of changes. Claude read the existing file before editing it each time, which meant changes were made in context rather than generating fresh code that would need to be merged manually.

The AI understood design intent

Asking for "an actual trashcan which pops up" instead of a red circle wasn't a technical spec -- it was a vibe. Claude interpreted that as: give it a real icon, animate it in with a scale transition, make it look like a floating action rather than an inline element. The result matched the intent without needing to specify border-radius, transition timing, or positioning manually.

Clarifying questions improved output

When Claude asked what the biggest pain point was before building anything, it avoided building the wrong thing. That single question made the first output more useful than if it had just guessed.


WHAT DIDN'T WORK PERFECTLY

The delete button hover area needed two attempts

The first version of the delete button only appeared when hovering over the right side of the task, not the whole row. This happened because the button was positioned inline in the flex layout. It took a follow-up prompt to fix -- moving it to absolute positioning so the whole task card could act as the hover trigger. The lesson: behavior that depends on layout often needs a correction round.

Default sample data used placeholder names

The initial sample tasks used generic fictional names (Alex M, Jamie L, Sam K) rather than the actual team members. This was fine for a prototype but meant the sample data had to be mentally ignored. In hindsight, specifying real team member names from the start would have made the demo more immediately useful.

localStorage means data doesn't sync between devices

The app saves tasks in the browser's local storage, which works great for a single person but means two team members opening the same HTML file on different computers see different data. This limitation wasn't discovered until after the core was built. A real shared backend (like Firebase or Supabase) would fix it, but was out of scope for this version.


HOW THE TOOL EVOLVED

Round 1 -- Initial prototype built from a single problem description
Round 2 -- Exported as a downloadable HTML file with git setup instructions
Round 3 -- Added delete button per task
Round 4 -- Replaced free-text assignee field with a dropdown of the 15 team members
Round 5 -- Added "All" option, redesigned delete button, added due time field
Round 6 -- README written for anyone discovering the project
Round 7 -- This file


THE BIGGEST TAKEAWAY

The bottleneck was never the code -- it was knowing what to ask for. Prompts that described a feeling or a problem ("deadlines get missed," "the button should pop up") worked better than prompts that described a solution ("add a CSS transition to the delete button"). The more clearly you can say what's wrong or what you want the experience to be, the less you need to know about how to build it.

The iteration loop was fast enough that it didn't feel like working with a tool. It felt like working with someone who could code.
