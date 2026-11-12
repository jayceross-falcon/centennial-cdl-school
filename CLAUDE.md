# CLAUDE.md: Centennial CDL School website

Read `docs/context.md` and `docs/research.md` before making changes. They hold the client's requirements, the brand notes and the open questions.

## Who you're working with

Jayce (Velocity Forge) directs the work but is not a developer. When you use a technical term (git, framework, hosting, deployment), add a short plain-English explanation in parentheses the first time it comes up. Keep the engineering itself at a senior-engineer standard; never pick a weaker approach because it's easier to explain.

## The client's rules (non-negotiable)

- **Premium, not AI-looking.** The client said AI-built sites "just look stupid." No generic template look: no identical rounded card grids, no gradient blobs, no cream-serif-terracotta or black-plus-neon palettes, no ALL-CAPS label over every heading, no abstract slogan headlines. Credibility comes from specifics (real trucks, real prices, real dates), not adjectives.
- **No AI-generated imagery or video.** Real photos and real footage only. Until the photographer shoots, use clearly marked grey placeholders, never stock or generated images.
- **Red brand, similar to centennialtrucking.com.** The exact red and fonts are not confirmed yet (see `docs/context.md`); keep colors in one set of variables so the real values can be dropped in.
- **Separate site.** Do not link to or embed centennialtrucking.com unless Jayce says the client approved it.
- **Request-info form goes to Anna**, who follows up leads by phone. Every lead must carry its source (UTM tags, Google Ads click ID, referring site) so the client can see which ad or search produced it.
- **Traffic tracking:** GA4, Google Search Console and Microsoft Clarity are the plan.
- **SEO plus AI-search visibility:** price and start dates stated plainly on the page, structured data (schema.org), a real FAQ, fast pages.
- **Optional online sign-up:** a Stripe seat deposit, not full tuition. Not decided yet.

## Stack

Recommended, **not yet decided by Jayce**: Astro (a framework that outputs fast plain HTML pages) hosted on Netlify. Treat it as a recommendation; confirm with Jayce before scaffolding the build.

## Guardrails

- Don't deploy, create hosting sites, buy anything, or install tools globally without Jayce's explicit OK.
- GoHighLevel (the CRM, customer-relationship software) is read-only: never change anything there without Jayce's explicit OK for that specific action.
- Never put secrets (API keys, passwords, tokens) in the code or in commits. Use environment variables.
- Placeholder facts in the wireframe (prices, start dates, address, school name) are not confirmed by the client. Keep them marked as placeholders.
