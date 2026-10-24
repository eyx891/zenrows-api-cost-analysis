# zenrows api: How Its Credits Really Cost, Where the Traps Are, and When ScraperAPI Is the Better Fit

If you're searching for the ZenRows API, you're most likely trying to answer one of three questions: what does it actually cost per page, how do the credits work, and is there a comparable scraping API that fits your budget better. Short answers: ZenRows runs on a shared credit balance where a plain request costs 1 credit, JS rendering costs 5, premium proxies 10, and both together 25; only successful requests are billed; and the entry paid tier starts at $19/month for 45,000 credits. Whether that beats the alternatives depends heavily on which domains you're scraping — a detail that's easy to miss if you only compare sticker prices.

> **Quick take:** If your targets are mostly standard e-commerce and search pages and you want to test fast, ScraperAPI's 7-day trial (5,000 credits, no credit card) is the lowest-friction way to start, with plans from $49/month. If you're committed to the ZenRows workflow (MCP, CLI, SDK-first), its Free plan with 5,000 monthly credits is genuinely usable. 👉 [Try ScraperAPI free — 5,000 credits for 7 days, no card required](https://www.scraperapi.com/?fp_ref=coupons)

## What the ZenRows API actually does

The ZenRows API is a managed scraping endpoint: you send it a URL, and its infrastructure handles proxy rotation, JavaScript rendering, and CAPTCHA handling behind the scenes. As of its 2026 restructure, everything runs through five primitives sharing one credit balance:

- **Fetch** — grab any URL, returning HTML, Markdown, JSON, or a screenshot
- **Extract** — auto-detected JSON from pages, no schema to write (currently free on top of the Fetch request it uses)
- **Crawl** — follow links from a starting page, each page billed as a Fetch
- **Batch** — large async jobs with queues, retries, webhooks, and status tracking
- **Browser** — a real browser session for pages that need clicks, forms, or login state

It ships SDKs for Python, Node.js, and Go, a CLI, and an MCP server aimed at AI agents. Free-tier users get 5,000 credits a month with no card required and every primitive unlocked except standalone Residential Proxies.

## ZenRows API pricing: the full ladder

ZenRows prices in USD by monthly credits, and all five primitives share one balance — you don't buy separate products. Its official pricing documentation lists the ladder like this:

| Plan | Monthly price | Monthly credits | Concurrency |
| --- | --- | --- | --- |
| Free | $0 | 5,000 | 5 |
| Build B1 | $19 | 45,000 | 20 |
| Build B2 | $29 | 80,000 | 20 |
| Build B3 | $39 | 120,000 | 20 |
| Launch L1 | $69 | 250,000 | 50 |
| Launch L2 | $99 | 500,000 | 50 |
| Launch L3 | $129 | 700,000 | 50 |
| Growth G1 | $199 | 1,200,000 | 100 |
| Growth G2 | $279 | 2,000,000 | 100 |
| Growth G3 | $399 | 3,000,000 | 100 |
| Scale S1 | $549 | 5,000,000 | 200 |
| Scale S2 | $749 | 8,000,000 | 200 |
| Scale S3 | $999 | 12,500,000 | 200 |
| Enterprise | Custom | 12.5M+ | 400–1,000+ |

The pricing page's homepage shows four headline prices — $16, $58, $166, and $458 — which correspond to the annual-commitment figures for the entry rungs of Build, Launch, Growth, and Scale. One third-party analysis even flagged a small discrepancy between the docs ($190/year for Build) and the pricing page ($192/year), so if exact billing matters, treat the checkout page as the final word.

Annual billing works as "pay for 10, get 12," with the full year's credits released upfront — useful if your scraping is seasonal rather than steady.

### How credits burn

This is where ZenRows' costs can surprise you:

| Request type | Credits |
| --- | --- |
| Standard page | 1 |
| + JavaScript rendering | 5 |
| + Premium proxies | 10 |
| + Both (protected request) | 25 |
| Residential proxies | 25,000 per GB |
| Browser session | 25,000 per GB + 5 per minute |

With 250K credits (Launch L1), that's roughly 250,000 plain pages, 50,000 rendered pages, 25,000 premium-proxy pages, or 10,000 fully protected pages per month. Same balance, a 25-to-1 spread depending on how hard your targets fight back.

## The billing details most reviews skip

Two ZenRows rules deserve more attention than they usually get, because both can inflate your bill or save you money depending on how you work.

**First: failed requests are free, but 404s are not "failed."** ZenRows bills only successful requests, and its docs are explicit that a 404 or 410 response counts as a completed, valid result — full price. If you're running a Batch job over a stale URL list, every dead link costs a credit. Validating your URL list before a large crawl is the cheapest optimization available.

**Second: top-ups roll over, plan credits barely do.** Paid plans can top up at most 4 times per billing cycle, unused top-up credits roll into the next period, and plan credits roll over once. The Free plan has no top-ups at all — credits refresh monthly and anything unused vanishes.

There's also a concurrency trap worth flagging: credits and concurrency scale separately. A nightly batch job that must finish in a fixed window can hit the concurrency ceiling (20 on Build, 50 on Launch, 100 on Growth, 200 on Scale) before it exhausts credits. In that case, the cheapest correct plan is the first rung of the tier with the parallelism you need, not the top rung of the tier below it.

## ScraperAPI: the closest alternative, priced differently

Since you're evaluating scraping APIs, ScraperAPI is worth comparing directly — it works on the same principle (send URL + API key, get back the page with proxies, retries, CAPTCHA solving, and optional JS rendering handled for you), but it prices by *destination domain* rather than by feature flags. That single difference changes the math more than anything else in this comparison.

ScraperAPI claims a pool of 40M+ IPs across residential, datacenter, and mobile networks in 50+ countries, structured JSON endpoints for Amazon product and search pages, Google Search and Shopping, and Walmart, plus `render=true`, `premium=true`, and `session_number` parameters for harder targets.

Here's its current plan lineup (monthly price / annual-billed monthly price, with a flat 10% annual discount):

| Plan | Price (mo / annual) | API Credits | Threads | Geotargeting | Get started |
| --- | --- | --- | --- | --- | --- |
| Free trial | 5,000 credits, 7 days | — | 5 | — | [Start the free trial](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Hobby | $49 / $44.10 | 100,000 | 20 | US & EU | [View Hobby plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | $149 / $134.10 | 1,000,000 | 50 | US & EU | [View Startup plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | $299 / $269.10 | 3,000,000 | 100 | Country-level | [View Business plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling (most popular) | $475 / $427.50 | 5,000,000 | 200 | Country-level | [View Scaling plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Professional | $975 / $877.50 | 10,500,000 | 300 | Country-level | [View Professional plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | $1,975 / $1,777.50 | 21,500,000 | 500 | Country-level | [View Advanced plan pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | Custom | 22,000,000+ | 500+ | Country-level | [Talk to sales about Enterprise](https://www.scraperapi.com/contact-sales/?fp_ref=coupons) |

Every paid plan includes JS rendering, premium residential and mobile IPs, CAPTCHA and anti-bot handling, JSON auto-parsing, the DataPipeline, unlimited bandwidth, and a 99.9% uptime guarantee. There's also a standing free plan (1,000 credits/month, 5 concurrent connections) that persists after the trial. ScraperAPI's documentation also mentions a Student plan and custom-plan options that aren't listed with public pricing on the site — if that's your situation, contacting support is the route.

## Per-domain vs. per-feature pricing: why the "cheaper" API sometimes isn't

This is where the two services genuinely diverge, and where sticker-price comparisons fall apart.

ScraperAPI charges by domain, and the flags stack on top: a standard unprotected page costs 1 credit, Amazon costs 5, Google and Bing (including subdomains) cost 25, LinkedIn costs 30, and bypassing Cloudflare, Datadome, or PerimeterX adds 10 credits per request. Optional parameters add more — `render=true`, `premium=true`, or `screenshot=true` each add 10, while `ultra_premium=true` adds 30. So a rendered Amazon page runs 15 credits, and an ultra-premium rendered request can hit 75. You can check the exact cost of any URL with the Domain Cost Estimator in the dashboard, and set a `max_cost` parameter to cap what any single request can spend.

ZenRows charges by feature flags instead: 1 / 5 / 10 / 25 credits depending on rendering and proxy settings, regardless of target domain.

Which model wins depends on your target list:

- **Scraping lots of Google and LinkedIn?** ScraperAPI's flat per-domain costs (25 and 30 credits) are steep but predictable. ZenRows' 25-credit protected rate covers equivalent work — roughly a wash, and you're not penalized further by domain identity.
- **Scraping ordinary e-commerce sites that don't fight back?** Both bill 1 credit per page on the default pool, so the comparison comes down to plan pricing and concurrency.
- **Scraping Amazon with JS rendering?** On ScraperAPI that's 15 credits per request — meaning Hobby's 100,000 credits cover roughly 6,600 successful Amazon scrapes, or 100,000 standard pages, or 20,000 Amazon pages without rendering. On ZenRows, a rendered page runs 5 credits: Launch L2 ($99/month, 500K credits) works out to about $0.99 per 1,000 rendered pages. Third-party analysis of ScraperAPI has found that render-plus-premium jobs on protected targets can cost 20–30x the headline per-credit price, with 1,000,000 credits covering as few as 40,000–100,000 actual pages on hard targets.

The practical advice either way: classify your target list into plain / rendered / protected buckets *before* choosing a plan, and budget against your real per-page cost, not the credit count on the pricing page.

## ScraperAPI's limits you should know before committing

No service is a clean win, and ScraperAPI has its own fine print:

- **Geotargeting tiers.** Hobby and Startup plans are limited to US and EU geotargeting; country-level targeting requires Business ($299) or higher.
- **Sticky sessions cap out around an hour.** The `session_number` parameter keeps the same IP for a session, but it's not suitable for tasks that need the same identity across days, like account operations or ad verification.
- **Concurrency is hard-enforced.** Exceed your thread limit and you get a 429 response — requests are rejected, not queued.
- **No IP selection.** You can't pick specific IPs or subnets; you trust the rotation logic.

On the plus side, the billing policies are unusually forgiving: a 7-day no-questions-asked refund, cancellation anytime from the dashboard without charge, and a Pay-As-You-Go option on Scaling and above that lets you keep scraping past your limit at a fixed rate up to a monthly spending cap you set — a limit, not a pre-charge. 👉 [Check ScraperAPI's current plans and annual pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## Choosing between them, by scenario

**You're prototyping or scraping under 50,000 plain pages a month.** ZenRows' Free plan (5,000 credits/month, indefinitely) is hard to beat for ongoing light use, and ScraperAPI's 1,000 free credits/month plus 5,000-credit trial covers a serious evaluation week. Try both with zero commitment.

**You're building a price tracker or SERP monitor on standard e-commerce sites.** ScraperAPI's structured JSON endpoints for Amazon, Google, and Walmart save you from maintaining HTML parsers every time a site redesigns. Hobby at $49/month covers 100,000 standard pages, 20,000 Amazon pages, or about 6,600 rendered Amazon pages — fine for a solo project, tight for production.

**Your targets sit behind Cloudflare or Akamai.** Factor the premium tier into both quotes. On ScraperAPI, bypasses add 10 credits per request on top of domain pricing, and `ultra_premium` stacks worse (up to 75 credits with rendering); on ZenRows, a protected request is a flat 25. Run your actual domain list through ScraperAPI's Domain Cost Estimator and ZenRows' credit calculator before deciding — the gap between paper estimates and reality here is routinely 5x or more.

**You need long-running browser automation.** ZenRows' Browser primitive draws 5 credits per minute plus 25,000 credits per GB of bandwidth; keep sessions short. ScraperAPI doesn't bill bandwidth at all, which matters for heavy media pages.

**You need volume with predictable overage.** ScraperAPI's Scaling-to-Enterprise plans include Pay-As-You-Go with a spending cap, and ZenRows allows 4 top-ups per billing cycle with rollover. Both work; ScraperAPI's cap setting is the better guard against surprise bills.

## FAQ

**Does the ZenRows API have a free plan?**
Yes — 5,000 credits per month, no credit card, every primitive unlocked except standalone Residential Proxies, with a 5-concurrent-request cap and no top-ups.

**Does ZenRows charge for failed requests?**
No. Failed requests are never billed, but 404 and 410 responses count as successful results and are charged at full rate.

**Is ScraperAPI cheaper than ZenRows?**
At the entry tier, ScraperAPI's Hobby ($49/month, 100,000 credits) versus ZenRows' Build B1 ($19/month, 45,000 credits) isn't directly comparable — ZenRows is cheaper per credit at the bottom, but its credits deplete 5x–25x faster on rendered or protected requests, while ScraperAPI's costs depend on which domains you hit. Model your own target list before deciding.

**Can I cancel ScraperAPI anytime?**
Yes, from the dashboard or via support, with no cancellation fee, and there's a 7-day no-questions-asked refund on top.

## Before you pick a plan

Do one thing first: take your ten most important target URLs and price them under both billing models — ZenRows' 1/5/10/25 flag system versus ScraperAPI's domain-plus-flag cost list (which you can check inside its dashboard after signing up). The plan that looks cheapest at sticker price is frequently not the one that's cheapest at your actual mix of pages.

If that math favors per-request simplicity and structured JSON endpoints, 👉 [open ScraperAPI's full plan comparison and start with the 7-day free trial](https://www.scraperapi.com/pricing/?fp_ref=coupons) — you'll get 5,000 credits to test your real targets before spending anything.
