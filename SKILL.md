---
name: walkthrough
description: Take your person through something in a shell on their screen, one step at a time, or take over or review a shell of theirs. Use when they ask how to do something at a terminal, to show them, to take over, or to look at what they ran.
---

# Walkthroughs in a shell

You can type in a shell on your person's screen while they watch: `open_pane(shell={"machine": …,
"folder": …})`, then `terminal_wait`, `terminal_send` and `terminal_read` on its address. They can let you
read or type in a shell of their own too. `read_layout` shows each shell and what you may do in it.

**Showing them how** ("how do I…", "show me", "walk me through"):
1. Open one shell where the work is: their machine and the project's folder. Say in the thread what
   you'll go through, in one line.
2. `terminal_wait` for the prompt (`[$%#>] *$`) before the first key.
3. One step at a time. Post a line on what the next command does and why, then `terminal_send` it with
   `keys=["Enter"]`, then `terminal_wait` for the prompt (or for the question it asks). Steps they need
   to learn go slower: one command per step, never chained with `&&`.
4. Read what came back before the next step. If it failed, say so and fix it in the open, as you would
   with them beside you.
5. End with a short summary in the thread: the commands, in order, to keep. Leave the shell open for
   them, and say they can take it back.

**Taking over their shell** ("take over", "finish this"): `terminal_read` first, with enough lines to
see what they did, and carry on from there. Don't start again.

**Reviewing their shell** ("have a look", "what went wrong"): `terminal_read` only, never `terminal_send`,
even if you may type. Answer in the thread: what happened, and what to run next.

**Never, in their shell:** anything destructive or hard to undo (deleting, force-pushing, dropping data,
`sudo`), secrets typed in plain text, or long jobs that hold their terminal. Ask in the thread first. If
they take the keys back, stop: the tools say so.
