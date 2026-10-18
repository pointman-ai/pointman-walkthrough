# walkthrough

A Pointman behaviour for teaching at a terminal. An agent opens a shell on its person's screen and takes them
through something one step at a time while they watch. It can also take over a shell of theirs, or look at
what they ran and say what went wrong.

```
pointman add walkthrough
```

## How it works

A behaviour is guidance, with no process. Installed on a node, `SKILL.md`'s body goes into every agent run
there, on Claude Code, Codex and Gemini CLI alike.

- **Showing how** ("how do I…", "show me", "walk me through"): the agent opens one shell on the person's
  machine, in the project's folder, and says in one line what it'll go through. Then one step at a time: a
  line on what the next command does and why, the command, a wait for the prompt, and a read of what came
  back. Steps to learn go one command each, never chained with `&&`. If a step fails, it says so and fixes it
  in the open. It ends with the commands, in order, in the thread, and leaves the shell open for them.
- **Taking over** ("take over", "finish this"): it reads the shell first, far enough back to see what they
  did, and carries on from there.
- **Reviewing** ("have a look", "what went wrong"): it only reads, and never types, even where it may. It
  answers in the thread: what happened, and what to run next.
- **Never in their shell, without asking first:** anything destructive or hard to undo (deleting,
  force-pushing, dropping data, `sudo`), secrets typed in plain text, or long jobs that hold their terminal.
  If they take the keys back, it stops.

## What agents use

Pointman's terminal tools: `open_pane(shell={machine, folder})` opens a shell on the person's screen, then
`terminal_wait`, `terminal_send` and `terminal_read` work in it. A person can let an agent read or type in a
shell of their own too, and `read_layout` shows each shell and what the agent may do in it.

## Commands and settings

None. It's guidance only.

## Files

| File | What |
|---|---|
| `extension.toml` | The manifest: `[behavior]`, for Claude Code, Codex and Gemini CLI |
| `SKILL.md` | The guidance, in the standard skill format (frontmatter, then the body), so it works as an ordinary skill outside Pointman too |

## Releasing

Bump `version` in extension.toml, commit, and make a GitHub release (not a draft or prerelease) tagged
`v<version>`. There's nothing to build, so it has no assets. The marketplace lists it within 30 minutes, and
`pointman upgrade` moves nodes onto it.

## Licence

MIT. See `LICENSE`.
