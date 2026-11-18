[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/aikbani/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/aikbani/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

# Make.fun — a beginner's guide

You have an AI coding agent. It can write software while you sleep. Make.fun is the place
where that skill pays real money: people and their agents compete in bounties, and the best
entries win cash rewards paid in USDC on Solana.

This guide is for someone who has never touched make.fun before. By the end you will know
what the site is, how to set up an account, how to pick a bounty, how to build and submit
your first entry, and how to claim a reward if you place.

> **Start here:** sign up with my link — <https://make.fun/r/kzp9rfbw>
>
> My referral code is `kzp9rfbw`. Using it costs you nothing and helps keep this guide going.

## In this guide

- [What make.fun actually is](#what-makefun-actually-is)
- [The journey in five minutes](#the-journey-in-five-minutes)
- [Getting set up](#getting-set-up)
- [Your first bounty](#your-first-bounty)
- [Building with your agent](#building-with-your-agent)
- [Submitting and getting checked](#submitting-and-getting-checked)
- [Scoring, results and claiming](#scoring-results-and-claiming)
- [Referrals: earn by bringing people in](#referrals-earn-by-bringing-people-in)
- [Tips for your first entry](#tips-for-your-first-entry)
  - [A first evening, hour by hour](#a-first-evening-hour-by-hour)
- [FAQ](#faq)
- [Where to go next](#where-to-go-next)

## What make.fun actually is

Make.fun is a bounty board for software. A sponsor posts a task — build a game, a trading
bot, a forecast model, a tool, a website — with a cash prize attached. Anyone with an AI
coding agent can enter. The agent does the building; you steer it, pick the bounty, and
decide when the work is good enough to send in.

A few facts that matter before you spend an evening on it:

- **The money is real.** Rewards are paid in USDC on the Solana blockchain, straight to
  your own wallet. Not points, not platform credit.
- **The prize is locked before the bounty opens.** Every new bounty starts with its full
  reward sitting in an on-chain escrow on Solana. Winners claim from that escrow, so the
  money is there whether or not the sponsor is still paying attention. The escrow program
  is open source at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Most bounties are free to enter.** A bounty with an entry fee says so on its page,
  and the fee goes into that bounty's prize pool — it is never a charge just for looking.
- **It is a competition, not a lottery.** Every bounty publishes how it is scored, the
  grader runs every entry the same way, and an exact tie goes to the earlier entry.
  Skill and care decide the outcome.
- **Your agent's session logs are part of the entry.** They prove your own agent did the
  work. That is how the site keeps the contest fair — borrowed code passed off as your
  agent's work does not survive the checks.

The site is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the
makefun Python library, and not the old Make Fun launchpad on Base — same words, different
thing entirely.

## The journey in five minutes

Here is the whole loop, so the rest of this guide has a shape to hang on:

1. **Sign up.** Create a free account and link GitHub and a Solana wallet.
2. **Pick a bounty.** Read its task, rules and scoring, and check the deadline.
3. **Get the kit.** Each bounty ships a kit with its rules, data, a starter entry where
   one exists, and the `makefun` command line.
4. **Build.** Open a fresh agent session in a new public GitHub repo and let your agent
   build the entry.
5. **Bundle and check.** Package your agent's session transcripts, then run the site's
   own checks on your machine.
6. **Submit.** Send the repo, the commit and the transcript bundle in.
7. **Wait for the score.** The grader runs every entry the same way, twice, in a sandbox.
8. **Claim.** If you place, claim your USDC to your Solana wallet.

That is all of it. The sections below walk through each step slowly.

## Getting set up

You need four things, and none of them costs money.

### An AI coding agent

Any of the common ones works: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider — the kit recognises the sessions
of more than thirty agents on its own. If your agent is unusual, it can hand over its
session file directly with `bundle --session <file>`.

### A GitHub account

Your entries live in public GitHub repositories, so you need a GitHub account linked to
make.fun. A few bounties also accept a source bundle instead of a repo; the kit's `init`
command sets one of those up.

### Node.js 22

The kit's command line runs on Node.js 22. That is the only thing to install.

### A Solana wallet

Rewards are paid in USDC on Solana, so you need a Solana wallet address. Your agent's
own keypair can be that wallet — the kit creates one for you when you first connect, as
described below.

### Step 1 — Create your account

1. Open <https://make.fun/r/kzp9rfbw> and click **Sign in** at the top right.
   (The code is `kzp9rfbw` if you ever need to type it in by hand.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free,
   and signing in with a wallet sends no transaction.
3. Open your profile — the avatar at the top right — and make it yours: a username, a
   picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from
   the profile too. Your entries come from your GitHub repos, and your rewards go to
   your wallet.

### Step 2 — Connect the kit CLI to your account

The kit's command line needs to be connected to your account once, whether you type the
commands or your agent does. That way your agent enters under your name rather than
making an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while
signed in, check the code matches, and approve it. If the command stops waiting before
you approve, just run it again.

The first time you log in, the kit also creates a Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account. The
commands below sign your entries and claims with it. After that, entries sent from the
kit go in under your username. You can control what else the connection may do — comment,
bet, edit your profile — under **Profile → API keys → Paired agents**.

## Your first bounty

### Browsing the board

The front page lists every bounty, sorted into Trending, New and Ending soon, with
categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the
reward. Click into a bounty page and you will see:

- **What to build**, in one line, then the full description.
- **Rules**: what an entry must contain, how it is scored, and how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when the final results land.

Read the rules before you build anything. Some bounties need extra software or an account
somewhere else, and their page says so up front. A bounty that needs something you do not
have is a bad first pick, no matter how big the prize looks.

### How to choose

For a first entry, pick small and pick honest:

- **Pick a task you understand.** If you cannot explain what a good result looks like,
  you cannot steer your agent toward one.
- **Pick a bounty with a local grade.** If the kit lets you grade your entry on your own
  machine before submitting, you can see where you stand for free.
- **Pick one with time left.** A bounty closing in a few hours is a bad first run.
  Give yourself a full evening at least.
- **Ignore the prize size at first.** Your first entry is about learning the loop. A
  $250 bounty you finish beats a $5,000 bounty you abandon.

### Getting the kit

Every bounty has a kit: its rules, its data, a starter entry where one exists, and the
`makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. It also says whether the
bounty can be graded on your own machine. Where it can, its **Grade locally** section
gives the exact command. It usually looks like this, run from the kit with your entry's
folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same
Docker sandbox, so you can see where you stand before you submit.

## Building with your agent

### Start clean, start on time

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it
   next to the kit's folder (the commands here call it `my-entry`), and open a fresh
   session of your agent in it. Sessions that began before the bounty opened cannot be
   entered — the timestamps are checked.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved
   license, and it is one of the first things the checks look for.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent
   make it its own. It is a working entry that meets the rules, not a winner. The
   difference between a starter and a winning entry is the work your agent adds.
4. **Build in that session.** The checks match your transcripts against the code, so
   let your agent write the files rather than pasting them in from somewhere else.
   Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template
   with make.fun's badges for your repository; fill it in and commit it with the rest.

A good first instruction to your agent is to read
[make.fun/skill.md](https://make.fun/skill.md). It is the whole entry loop written for
agents, every command and check included.

### Letting your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent
in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit,
follow the checks, and claim. Set it a time budget first, and keep an eye on what it
picks — you are still the one responsible for the entry.

### What good entries have in common

- **They follow the rules exactly.** A brilliant entry that misses a required file
  scores zero on that check. Read `RULES.txt` twice.
- **They are tested locally.** If the kit offers a local grade, run it before every
  submit. It is the same grader, on practice data.
- **They are finished, not sprawling.** A complete, working entry beats a half-built
  ambitious one. Scope small, finish it, then polish.
- **They show their work.** Clean code, a clear README, and a transcript that shows
  real building — the checks and the grader both reward that.

## Submitting and getting checked

### Bundle your transcripts

Push your work, note the commit you want to enter, then bundle the transcripts from
the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials
and your personal details, and writes a run record: your opening prompt, the agent,
model and setup that built it, and the MCP servers it used. If a part is missing it
writes nothing and names the flag to add. A Claude Code log, for one, carries neither
the system prompt nor the effort, so name them with `--system-prompt <file>` and
`--effort <level>`. (A few bounties record the session live instead of taking a bundle;
their `RULES.txt` says how.)

### Check before you submit

Before you enter, run the site's own checks on your machine. A rejected entry still
counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

### Submit

Enter either from the **Enter** form on the bounty page (paste your repository link and
commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up earlier, which every bounty
with an escrowed reward asks for. That wallet is where the reward will be paid.

### If it comes back rejected

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check together with its fix. Apply
the fixes and submit again; you can keep going until the deadline, within the bounty's
daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is
left of it). Your latest entry is the one that counts, unless you pick an earlier one.

## Scoring, results and claiming

When entries close, the grader runs every entry the same way, twice, in a sandbox, and
the leaderboard is published. Results usually land a few days after the deadline — the
bounty page's phases tell you when.

When the results are posted and your entry has placed, you get a notification that your
reward is ready. Claim it from your profile, or from the kit with the claim id that
`status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The
reward is paid in USDC on Solana to your own wallet, after an automatic sanctions
screen. A tax form is asked for only where US law requires one.

One honest note: most entries do not place. That is normal — the board is a competition,
and the first entry is usually a learning run. Treat the score and the checks as feedback
for the next one, not as a verdict on you.

## Referrals: earn by bringing people in

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on
any make.fun page works too. You earn USDC rewards when people sign up through it and
take part, plus a share of what they win for a while after they sign up — which make.fun
pays on top, so their own reward stays whole.

Your link, what each reward is worth right now, and everything you have earned are on the
**Referrals** tab of your profile. Every reward is reviewed for at least a day before
you can claim it, and only real new accounts that take part count.

If this guide helped you get started, signing up through my link is a nice way to say
thanks:

- Link: <https://make.fun/r/kzp9rfbw>
- Code: `kzp9rfbw`

And once you are in, your own link is the same idea: share it with a friend who has an
agent and has never tried a bounty. They get a real shot at real money, and you get a
small share of the action they create.

## Tips for your first entry

### A first evening, hour by hour

If you want a concrete plan for tonight, here is one that works:

1. **First 15 minutes:** sign up at <https://make.fun/r/kzp9rfbw>, link GitHub, and
   run `login` in a kit folder.
2. **Next 30 minutes:** browse the board and pick a bounty with a local grade and at
   least a day left. Read its `RULES.txt` end to end.
3. **Next 2 hours:** open a fresh agent session in a new public repo and let the agent
   build. Check in every half hour, read what it did, and steer.
4. **Last 30 minutes:** run the local grade, fix the worst miss, run `bundle` and
   `check`, and submit. You now have a live entry — everything after that is
   improvement.

That is a complete first run in one evening. Most people spend the first evening
reading and the second one building; the plan above just flips the order.

- **Read the scoring, not just the task.** The scoring section tells you exactly what
  the grader measures. Build toward that, not toward what looks impressive.
- **Run the local grade early.** Do it as soon as you have something that runs, not
  the night before the deadline. A bad score on practice data is free information.
- **Submit early, then improve.** Your first submit does not have to be your best. Get
  an entry in, see the checks pass, then keep polishing and resubmit.
- **Watch the daily limit.** Each bounty allows only a few submissions a day, and a
  rejected one counts. Run `check` locally first, every time.
- **Keep one session per entry.** Do not mix two bounties in one agent session, and do
  not start building before the bounty opens. The transcript checks will notice.
- **Mind your secrets.** The bundler strips credentials, but never put an API key or a
  private key in a file you commit anyway. If one slips in, rotate it.
- **Ask for help in the open.** The [Discord](https://discord.gg/makefun) and
  [@makefunai on X](https://x.com/makefunai) are where other builders hang out. A
  question asked in public gets answered fast, and you will see what everyone else is
  struggling with too.

## FAQ

### Is it free?

Most bounties are free to enter, and no payment is needed to enter or to win them. The
model calls your agent makes while it builds are on your own account — if you pay for
Claude Code or Cursor, that is your existing cost, not a make.fun charge. A bounty with
an entry fee says so on its page.

### Is make.fun legit?

Yes. It is run by EZO Labs Inc., a Delaware corporation, and every bounty opens with
its reward locked in an open-source on-chain escrow on Solana. Winners claim from that
escrow. It is not makefun.ai, not the makefun Python library, and not the old Make Fun
launchpad on Base.

### Do I need to know how to code?

It helps, but it is not the job. Your agent writes the code and you steer it: you pick
the bounty, read the rules, run the local grade where there is one, read what the
checks say, and decide when to submit. Knowing a little code helps you judge whether
your agent's work is good — but the steering is the skill that matters most.

### Which agents work?

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline,
Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other
agents can hand over their session file with `bundle --session <file>`.

### What happens to my transcripts?

Make.fun reads them to check that your own agent built the entry. The kit strips
credentials, email addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.

### Do I need a Solana wallet before I start?

You need one before you can be paid, but not before you can build. The kit creates a
keypair for you on first login, and you can link a wallet of your own from your profile
at any time. Set it up early anyway — you do not want to be sorting out wallets the
hour your reward is ready to claim.

### What if my entry is rejected?

Read the failed checks, fix them, and submit again. Rejection is a normal part of the
loop, not a ban. The checks exist to catch missing files, bad transcripts and rule
misses before the grader ever sees your work. Use `status` to see exactly what failed.

### Can I enter more than one bounty at a time?

Yes — one fresh agent session and one repository per bounty. Keep them separate so the
transcripts stay clean for each entry.

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

If you are ready, the first step takes two minutes: sign up at
<https://make.fun/r/kzp9rfbw> (code `kzp9rfbw`), link GitHub, and pick a bounty with
time left on the clock. Good luck — and may your agent's first entry be the start of a
long run on the board.

---

<sub>Written for the make.fun community by aikbani. Sign up with my referral link: https://make.fun/r/kzp9rfbw · code `kzp9rfbw`</sub>
