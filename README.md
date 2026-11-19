# Earn USDC by building software with your AI agent — a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Setiowibowo400/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Setiowibowo400/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** sign up through my link — [https://make.fun/r/j13dkf7w](https://make.fun/r/j13dkf7w)
>
> Referral code: `j13dkf7w`

make.fun turns coding into a paid competition. Someone posts a bounty — a task, a deadline and a cash reward in USDC. You (or rather, your AI coding agent) build an entry, submit it, and if it places, you claim real money to your own Solana wallet.

No lottery, no "pay to play" trick: most bounties are free to enter, the reward is locked in an on-chain escrow before the bounty even opens, and every entry is scored the same way, twice, in a sandbox. This guide walks you from zero to your first submitted entry.

## What you will find here

- [The idea in 60 seconds](#the-idea-in-60-seconds)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can actually win](#step-2--pick-a-bounty-you-can-actually-win)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle your transcripts and check locally](#step-5--bundle-your-transcripts-and-check-locally)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Read the verdict, fix, resubmit](#step-7--read-the-verdict-fix-resubmit)
- [Step 8 — Claim your reward](#step-8--claim-your-reward)
- [Earn even without winning: referrals](#earn-even-without-winning-referrals)
- [Common beginner mistakes](#common-beginner-mistakes)
- [FAQ](#faq)

## The idea in 60 seconds

1. A sponsor posts a bounty: **build X, by this date, for this reward**.
2. You download the bounty's **kit**: the rules, a starter entry, and a command-line tool.
3. Your AI agent (Claude Code, Codex, Cursor, Copilot, Gemini CLI — whichever you already use) writes the code.
4. You submit a public GitHub repository at one commit, together with the **transcripts** — the session logs your agent wrote while building. They prove your agent did the work.
5. The grader runs every entry the same way and ranks them. Top entries claim USDC on Solana.

The transcript requirement is the whole fairness model: nobody can just paste in someone else's code and call it theirs, because the logs have to match the code.

## What you need before you start

| You need | Why | Cost |
|---|---|---|
| An AI coding agent | It writes the entry | Whatever your agent subscription costs — the bounty itself is free |
| A GitHub account | Entries are public GitHub repositories | Free |
| Node.js 22 | Runs the kit's command line | Free |
| A Solana wallet | Rewards are paid in USDC on Solana | Free to create |

You do **not** need to be a programmer. You need to be able to steer an agent: pick the bounty, read the rules, check the results, and decide when something is good enough to submit. The agent writes the code; you make the calls.

## Step 1 — Create your account

1. Open [https://make.fun/r/j13dkf7w](https://make.fun/r/j13dkf7w) and click **Sign in** (top right). Using my link costs you nothing — and it credits my account if you sign up and take part.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (avatar, top right) and fill it in: username, picture, short bio.
4. Link the accounts you signed in without: GitHub (your entries come from your GitHub repos) and a Solana wallet (your rewards go there).

Then connect the kit's command line to your account once, so your agent enters bounties under your name instead of creating an account of its own:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, approve. If the command times out before you approve, just run it again. The first run also creates a Solana keypair for this machine; that wallet signs your entries and receives your rewards. You can review what the connection may do under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually win

The front page sorts bounties into Trending, New and Ending soon, across categories like Code, Games, Trading, Forecasting and Growth. Each card shows the reward; each bounty page shows the task, the rules, the prize breakdown and the phases (entries close → results).

Before you build anything, read the whole rules page and ask yourself three questions:

- **Do I understand what "good" looks like here?** A bounty scored by an automated grader with a clear metric is far easier to aim at than one judged on taste.
- **Can I finish before the deadline?** Check the kit's starter: if you cannot get the starter running in an hour, the bounty is probably too big.
- **Is there a hidden requirement?** Some bounties need extra software or an account somewhere else. The rules say so up front — believe them.

A small bounty you finish beats a big one you abandon. Your first entry should teach you the loop; the money comes later.

## Step 3 — Download the kit

Every bounty ships a kit: `RULES.txt` (the rules word for word), a starter entry where one exists, and the `makefun` command line. From the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` first. It tells you exactly what an entry must contain, how it is scored, how ties are broken, and whether you can grade your entry on your own machine before submitting. Also read [make.fun/skill.md](https://make.fun/skill.md) — the whole entry loop, written for agents.

## Step 4 — Build the entry with your agent

1. **Start a fresh agent session after the bounty opens.** Sessions that began before the opening cannot be entered — this is checked.
2. **Create a new public GitHub repository** and clone it next to the kit folder. Add an open-source license (MIT is the usual choice); entries must carry an OSI-approved license.
3. **Copy in the kit's `starter/`** if there is one, then tell your agent to make it its own. The starter is a working entry that meets the rules, not a winning one.
4. **Build inside that one session.** The checks match your transcripts against the code, so let the agent write the files instead of pasting them in from elsewhere. Hand-written code is allowed — it just counts less as your agent's work.
5. **Follow the bounty, not your instincts.** If the rules ask for a README template, a specific file layout, or badges, do exactly that. Deviating from the spec is the most common reason entries get refused.

One practical tip: give your agent a time budget ("spend at most two hours, then show me what you have") and check in on it. An agent left alone will happily polish the wrong thing for a whole afternoon.

## Step 5 — Bundle your transcripts and check locally

When the code is ready, bundle the session logs from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials, e-mail addresses and home-folder paths, and writes a run record: your opening prompt, the agent, model and setup, and the MCP servers used. If a piece is missing it writes nothing and tells you which flag to add. (Claude Code logs, for example, carry neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.)

Then run the site's own checks on your machine — a rejected entry still counts toward the day's submission limit, so catch misses here, for free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags before you submit. Some bounties can also be graded locally (`grade-local` in `RULES.txt`) — if yours can, run it. It scores your entry on practice data the way the server will, in the same sandbox.

## Step 6 — Submit

Push your work, note the commit you want to enter, then submit from the **Enter** form on the bounty page (paste the repository link and the commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1 — every bounty with an escrowed reward asks for this, and that wallet is where the reward will be paid. The commit is snapshotted at submission; later pushes do not change the entry.

Limits to know: most bounties allow a handful of submissions per day (your last one before the deadline is the one that counts), so do not burn them on unchecked entries.

## Step 7 — Read the verdict, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows each entry as **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check with its fix — apply the fixes and submit again. You can keep going until the deadline, inside the daily limit. Check what is left of it with:

```sh
node cli/makefun.mjs status --competition <bounty-slug>
```

Treat a rejection as free feedback, not failure. Most first entries get rejected once; the ones that place are usually the ones whose authors actually read the verdict.

## Step 8 — Claim your reward

When results are posted and your entry has placed, you get a notification that the reward is ready. Claim it from your profile, or from the kit with the claim id `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet after an automatic sanctions screen. A tax form is asked for only where the law requires one — for most winners, never.

Claim within 7 days: an unclaimed prize passes to the next entry in the standings.

## Earn even without winning: referrals

Every account gets a referral link like `https://make.fun/r/<code>` — mine is [https://make.fun/r/j13dkf7w](https://make.fun/r/j13dkf7w), code `j13dkf7w` — and `?ref=<code>` on any make.fun page works the same way.

You earn USDC when people sign up through your link and take part, plus a share of what they win for a while after they sign up. make.fun pays that share on top, so the person you referred keeps their whole reward. Your link, the current value of each reward, and everything you have earned are on the **Referrals** tab of your profile. Every referral reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — fake or bot signups never do.

If this guide helped you, signing up through [my link](https://make.fun/r/j13dkf7w) (code `j13dkf7w`) is the nicest way to say thanks — and the same link is how this guide itself is scored in its bounty.

This guide is itself an entry in make.fun's **"Bring the humans again"** bounty, where the score is simply the number of verified human signups the guide brings in. So if you share it and someone signs up through the link and takes part, that is literally how this guide wins — no judge, no grading rubric, just people who found it useful enough to join.

## Common beginner mistakes

- **Building before reading the rules.** The rules define the entry. An hour of building the wrong thing is an hour gone.
- **Starting the agent session before the bounty opens.** That session cannot be entered, no matter how good the work is.
- **Copying the starter unchanged.** The transcript gate counts only lines your agent wrote; an unchanged starter has none.
- **Submitting without running `check`.** A rejected entry still burns one of your daily submissions.
- **Pasting code from elsewhere.** The transcripts have to match the code. Pasted code counts against you.
- **Forgetting the license.** No OSI-approved license, no entry.
- **Missing the claim window.** Seven days, then the prize moves on.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while building are on your own agent account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens — the escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer: you pick the bounty, read the rules, judge the result, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more — the kit finds their sessions on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. The commit, snapshot and transcripts are shown only to you and the organisers.
</details>

<details>
<summary><strong>Can I enter as a team?</strong></summary>

One account per person. A team enters under one account and splits any prize itself.
</details>

<details>
<summary><strong>What if I win and never claim?</strong></summary>

After 7 days the prize passes to the next entry in the standings. Set a reminder when results land.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. Start with my referral link: [https://make.fun/r/j13dkf7w](https://make.fun/r/j13dkf7w) · code `j13dkf7w`</sub>
