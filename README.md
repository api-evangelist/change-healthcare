# Change Healthcare (change-healthcare)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Change Healthcare was one of the largest healthcare technology and clearinghouse companies in the United States, moving eligibility, claim, remittance and prior-authorization transactions between providers and payers over X12 EDI. UnitedHealth Group acquired it in October 2022 and folded it into Optum, and the brand has since been retired: `www.changehealthcare.com` redirects to `business.optum.com`, `developers.changehealthcare.com` redirects path-for-path to `developer.optum.com`, and the `apis.changehealthcare.com` API gateway is decommissioned and documented by Optum as "an old domain and no longer supported". The Change Healthcare Medical Network APIs — Eligibility v3, Professional Claims v3, Institutional Claims v1, Claim Status v2, Claims Responses and Reports v2, Attachments, PayerList v1 and Prior Authorization v1 — are still operated and documented, but on Optum infrastructure and under Optum hosts, and are catalogued in [`all/optum`](https://github.com/api-evangelist/optum) rather than duplicated here.

## Not published by Change Healthcare

Verified 2026-08-15 — recorded absences, not gaps in our research:

- **No OpenAPI, AsyncAPI, GraphQL SDL or MCP server** on any `changehealthcare.com` host. Every path on `apis.changehealthcare.com` and `sandbox.apis.changehealthcare.com` answers `400 {"error":"invalid_request"}`; `api.changehealthcare.com` resolves but times out on port 443; `developer.changehealthcare.com` is NXDOMAIN.
- **No `/.well-known/` document** on any host — see `well-known/change-healthcare-well-known.yml`.
- **No A2A agent card** at `/.well-known/agent-card.json` or the legacy `/.well-known/agent.json`.
- **No first-party SDK** on npm, PyPI, RubyGems, crates.io, NuGet, Maven Central or pkg.go.dev. `github.com/changehealthcare` is an empty personal **user** account with 0 public repos, not a company organization.
- **No published pricing and no published rate limits** — see `plans/` and `rate-limits/`, both recorded at count 0.
- **No security.txt, vulnerability-disclosure page, bug bounty or trust center.**

The one machine-readable document the company still serves is `https://www.changehealthcare.com/llms.txt` (HTTP 200) — an AI-usage policy marking every usage class disallowed, saved verbatim under `llms/`.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/change-healthcare/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Healthcare, Technology, Analytics, EDI, Claims, Eligibility, Clearinghouse, Revenue Cycle Management, Prior Authorization

## Timestamps

- **Created:** 2026-04-19
- **Modified:** 2026-08-15

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
