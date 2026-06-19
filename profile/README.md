# Tokarix

Tokarix is where I host my AI agent tooling. Three Rust projects:

- **[memory-server](https://github.com/tokarix/memory-server)** — semantic memory for AI agents. Store, search, and maintain durable memories with graph-based expansion, review workflows, and an offline dream/consolidation cycle. Exposes an MCP interface.
- **[forge-mcp](https://github.com/tokarix/forge-mcp)** — multi-forge, policy-enforcing MCP server that gives agents controlled access to Git forges (Forgejo, Gitea, GitLab). Fine-grained policy engine, audit trail, branch prefix enforcement.
- **cockpit** — operator dashboard and orchestrator for multi-project, multi-agent work. Coordinates agents, manages task lifecycles, renders plans, dispatches reviews. *Not yet published.*

## Why

Ehr... where do I even start.

In January 2026 I started experimenting with Google Antigravity on an AI Pro plan. Built some cool things. When it expired, I took a Claude Max plan. Used it with OpenClaw until I learned it violated the Claude Max plan policy. It was around that time — late February 2026, while using OpenClaw with my Claude subscription — that I vibe-coded the initial `memory-server`. I wanted the memories to live in something other than a text file.

Then I used Claude Code for about two months, also for a paid consulting project (client agreed I use Claude Code). That's where things got interesting. I had VPN access to the client on my workstation. But being paranoid, I would never run or give any agent or LLM direct access to my workstation. Add on top of that that Claude Code is closed source, so my distrust was... let's just say significant.

My setup: Fedora Kinoite immutable VM in an isolated VLAN on a host with HT disabled to protect against CPU vulnerabilities. I would create a bare repo on the VM, run agents in a toolbox on Kinoite. Push/pull to and from customer on-prem GitLab via my workstation, to the bare repo on the VM. A lot of manual labor.

We soon found out Claude Code alone was awesome, but at the same time often overlooked certain parts. We ended up making a plan with Claude, and letting Codex review it. By manually steering both: write a plan, review the plan at `$PATH`, etc.

I expanded `memory-server` to do the review via it. Still manual steering of agents though. Like the manual sync to and from GitLab/Kinoite. Manual repetitive work.

That's when I built `forge-mcp`. I wanted to give agents direct but controlled access to Git forges. There were existing MCP servers for this, but none of them had proper fine-grained access or policy control.

And again I found myself manually steering agents to use `memory-server` and then `forge-mcp`. Even more repetitive work. So I ended up building `cockpit`.

## The takeaway

After months of steering agents: they can not be trusted. Full stop. Doesn't matter how strict your prompts are. They will forget to run `cargo fmt`. They will skip `clippy`. They will ignore explicit rules like "never open a new PR to supersede an old one" and do it anyway. The entire reason `cockpit` exists is to impose structure that agents refuse to follow on their own.

## Issues & PRs

Disabled on these GitHub repos. Development happens on an internal Forgejo instance. `cockpit` will be published here when it's ready.

## Contact

If you're interested in the projects or want to work together, reach out via email: stijn@linux-ipv6.be
