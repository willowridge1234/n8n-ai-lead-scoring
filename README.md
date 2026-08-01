# AI Lead Scoring for n8n — score scraped leads against your ICP, free workflow

A working [n8n](https://n8n.io) workflow that takes leads from an Apify actor, has an LLM
score each one from 1–10 against **your** ideal customer profile with a one-line reason,
and appends every result to a Google Sheet.

Free to download and use. No signup wall, no disabled nodes, no "upgrade to unlock" stubs —
it is a complete working flow on its own.

**Download:** [`workflow/ai-lead-machine-free.json`](workflow/ai-lead-machine-free.json) —
or get it from [Gumroad](https://willowridge7.gumroad.com/l/ai-lead-machine-free) if you
prefer.

---

## What it actually does

1. Runs on a schedule you set.
2. Calls an Apify actor you choose and pulls that run's dataset.
3. Normalises the results into one consistent lead shape, dedupes them, and caps the batch.
4. Sends each lead to an OpenAI-compatible endpoint, which returns a **1–10 fit score** and
   a short reason.
5. Appends every lead — including the low scorers — to your Google Sheet.

Low scores are logged deliberately. If you only keep the winners you have no way to tell a
badly-tuned profile from a genuinely thin lead list.

## What you need

Three credentials:

| # | Credential | Used for |
|---|---|---|
| 1 | Apify API token | pulling the lead dataset |
| 2 | An OpenAI-compatible API key | the scoring call |
| 3 | Google account (OAuth) | writing to your sheet |

Plus an n8n instance — cloud or self-hosted, both work.

The scoring node is a plain HTTP request, so any OpenAI-compatible endpoint works. You are
not locked to one provider.

## Setup

1. Import `workflow/ai-lead-machine-free.json` into n8n.
2. Open **Your settings (EDIT ME)** and fill in your ICP description, your offer, and the
   max leads per run.
3. Open **Fetch fresh leads (Apify)**. Replace `YOUR-USERNAME~YOUR-ACTOR` in the URL with
   your actor ID, and replace the empty `{}` body with that actor's own input parameters.
4. Connect the three credentials above.
5. Paste your Google Sheet URL into the Sheets node.

Every node has a sticky note next to it explaining what it does.

### Which Apify actor?

Any of them — but the input body is specific to whichever actor you pick, so you supply
that actor's own parameters. It does not work unmodified with an arbitrary actor.

The workflow ships with a labelled worked example using our own
[New Liquor License Leads](https://apify.com/rook-data-tools/new-liquor-license-leads)
actor (new TX & CA restaurant/bar openings) if you want something that runs immediately.
Swap it for any other actor whenever you like.

## Paid edition

There is a [paid edition ($49)](https://willowridge7.gumroad.com/l/ai-lead-machine-n8n)
that adds a personalised opening line per lead, a qualified-only Slack digest, a Gmail
variant, a setup guide with a troubleshooting table, and an agency licence covering
unlimited client deployments.

The free version here is not crippled to sell you that. If it does what you need, use it.

## Licence

Free to use and modify for your own business or your clients' businesses, including
agencies deploying it for unlimited clients.

**Not open source.** You may not resell, redistribute, sublicense, or repackage the
template itself as your own product. See [LICENSE.txt](LICENSE.txt).

## Honest status

This was published recently and has no reviews, no ratings, and no user testimonials yet.
Nothing on this page is a claim about results other people have gotten — there aren't any
to report. Try it and judge it on what it does.

Built by [Rook Data Tools](https://apify.com/rook-data-tools).
