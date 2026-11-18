# openbar

**Your coding agents, in a bar at the edge of your screen.**

openbar is an open source desktop bar for the coding agents you already use. It runs them in the background and gives each session a small pill at the edge of your screen. From the pill you can approve a command, review a diff or send a reply, with no terminal open.

> **Status: early.** This README describes what openbar is being built to do. There is no release yet.

## What it does

- **One pill per session.** A ring on the pill shows the session's state: running, waiting for you, done, or failed.
- **A panel when you need it.** Open a pill to see:
  - what the agent is doing right now;
  - the command or file change it's asking to make, with the diff;
  - a box to reply in.
- **Approve or deny in one click.** The agent waits while you decide. Several agents can work at once, each in its own project.

## How it works

openbar is not an agent and has no harness of its own. It finds the agent CLIs already installed and signed in on your machine, and drives each one through the structured interface that CLI provides for this:

| Agent | How openbar talks to it |
|---|---|
| Claude Code | Headless mode with streaming JSON, plus a permission prompt tool that routes approvals to the pill |
| Codex | Its app server |
| Gemini CLI | The Agent Client Protocol (ACP) |

This means:

- **No terminal scraping.** openbar reads structured events, not screen output.
- **Your setup, unchanged.** Each agent uses your own install, sign-in, model and settings. openbar holds no API keys and has no account of its own.
- **The agent's own sandbox.** Commands run under each CLI's own permission and sandbox rules. openbar shows you the request and passes back your answer.
- **Sessions kept apart.** Each session can run in its own git worktree, so parallel agents don't edit the same checkout. Each session runs in its own process group (a Job Object on Windows), so stopping a session stops everything it started.
- **Local only.** openbar has no server. It sends nothing anywhere; the agents talk to their own providers as they normally would.

## Platforms

| Platform | Shape |
|---|---|
| macOS (first) | A compact island under the menu bar. Idle agents shrink to their ring, and panels drop down. ⌥ Space brings it up. |
| Windows | A bar along the screen edge. Panels pop up from the pills. |
| Linux | A floating top bar made for tiling setups. Super + Space brings it up. |

openbar is built with [Tauri 2](https://tauri.app): a Rust core and a web UI.

## Roadmap

1. Claude Code and Codex on macOS: start a session, stream its events, and handle approvals.
2. The bar itself: pills, panels, diffs and replies.
3. Gemini CLI over ACP.
4. Windows and Linux.

## Using a subscription plan

Each agent runs under its provider's own terms. If you use one through a subscription plan rather than an API key, check that provider's terms on driving its CLI from another app.

## Contributing

Ideas and issues are welcome now. Code lands here starting with the first milestone.

## License

MIT. See [LICENSE](LICENSE).

---

openbar is an independent project. It is not affiliated with or endorsed by Anthropic, OpenAI or Google. Claude Code, Codex and Gemini CLI are their owners' products.
