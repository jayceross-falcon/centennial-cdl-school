# Centennial CDL School website: research report

Prepared Nov 12, 2026 for Jayce (Velocity Forge). Read-only research: nothing installed, published, sent or bought. Brand notes from the current Centennial site are in `context.md` next to this file.

Labels used below: **[verified]** = I read it on the source today. **[inference]** = my reasoning, not checked. **[ask client]** = only Centennial can answer.

---

## 0. The short version

- **Top recommendation:** build a fast, photo-led site in **Astro** (a website framework that outputs plain, very fast pages), hosted on **Netlify**, with leads going into **GoHighLevel** (or a simple email form if you don't want to run their CRM). Use the Anthropic frontend-design skill plus **Impeccable** as the "anti-AI-look" quality gate, and the **official GSAP skills** for any motion.
- **The real bottleneck is not the wow factor.** It's (1) the price and start date being visible, (2) Anna calling leads within minutes, and (3) a Google Business Profile for the Lindon campus. A gorgeous site that hides the price loses to a plain one that shows it.
- **Video idea verdict:** as pitched (AI-generated cab interior, "exploding" on scroll) **3/10**. It works against the client's one hard rule. Reworked as a real 3D render of the truck's inspection systems, tied to the CDL pre-trip test, it's a **7/10**. Section 3 has what makes it a 10 and three cheaper alternatives.
- **Competitive reality check:** MTECH (state tech college, Lehi/Heber) charges **$1,820** total for Class A but has a waitlist **[verified]**. The Trucking School (Spanish Fork) charges **$4,400 for 3 weeks** **[verified]**. "Priced below market" only works against private schools; Centennial can't out-cheap MTECH, so the pitch has to be **start soon + a real trucking company behind you + a job path**.

---

## 1. What I found on centennialtrucking.com (summary)

Full notes in `context.md`. Highlights:
- The site is now live and finished (built on Duda by an agency, RedRaven AI). The earlier note about a temporary Bluehost address and placeholder text is **out of date** **[verified, 8 pages read]**.
- Brand: woman-owned, DBE/WBE/WOSB certified, Orem-based heavy civil hauler with a strong project list (SLC airport, I-15, Hill AFB, Rio Tinto). Values: Care, Safety, Integrity, Hard Work, Teamwork.
- Logo is black and silver with truck outlines. The client calls the brand red. **I could not read exact hex colors or fonts** (the page reader returns text, not styling). Two-minute fix: eyedrop it in Chrome, or ask the client for their brand file.
- Good: real photos, real projects, certifications up front, clear "Get a Quote" CTA.
- Weak: abstract slogan headlines ("Driven by Reliability. Built on Trust."), unattributed testimonials, a careers page that lists "CDL Truck Driver" with no pay and no way to get a CDL. **That gap is the school's story:** the school is how you get from "no CDL" to that job.

---

## 2. Skills, repos and techniques for a premium, non-generic site

### 2a. How to read star counts
Several design-skill repos jumped to 50k-150k stars within months. Stars on AI-skill repos are partly hype and are not a quality signal on their own **[inference]**. I weighted: who made it, whether it checks its own output, license, and whether it fits a real client build.

### 2b. Claude Code design skills

| Skill | What it does | Stars / license / last update | Verdict |
|---|---|---|---|
| **Anthropic frontend-design** (anthropics/skills) | Makes the agent plan a color/type/layout system for *this* subject before coding, and names the common AI tells (cream + serif + terracotta, black + one neon accent, identical rounded cards, ALL-CAPS labels over every heading, one italic word in a headline). | ~194k / repo has per-skill terms / Nov 6, 2026 | **Use.** Already built into this Claude setup. It's the baseline brief-writer. |
| **Impeccable** (pbakaus/impeccable) | 24 commands (`critique`, `audit`, `polish`, `typeset`, `bolder`, `quieter`...) plus a **deterministic AI-slop detector** (62 rules, no AI involved) that can scan a live page. Writes `PRODUCT.md` / `DESIGN.md` so every session follows the same rules. | ~109k / Apache-2.0 / Nov 12, 2026 | **Use as the quality gate.** Run `detect` on every page before the client sees it. **Do not use its "live" mode**: its README says it can fall back to running a coding CLI with approvals and sandboxing turned off. |
| **Hallmark** (Nutlope/hallmark, by Together AI) | Builds self-contained pages from 50 "material" themes, then lints them in a real browser at 8 screen widths against AI tells. Uses openly licensed Wikimedia photos. | ~54k / MIT / Nov 11, 2026 | **Borrow the linter, not the builder.** Its output is one-file HTML pages and its photo library is generic; we have real photos and want a proper component build. Its `sloplint --render` is a good second opinion. |
| **Taste Skill** (Leonxlnx/taste-skill) | Art-direction skill: reference images, one design system, browser check. Needs Node 22 + Chrome. | ~114k / MIT / Nov 8, 2026 | **Optional.** Overlaps with frontend-design + Impeccable. Useful for the moodboard step if the first directions feel flat. |
| **Emil Kowalski skills** (emilkowalski/skills; ex-Vercel/Linear design engineer) | Motion quality: `animate`, `review-animations`, `remove-animations`, `animation-performance`, `mobile-native` (fixes iPhone tap delays, 100vh bug, input zoom). | ~56k / MIT / Nov 12, 2026 | **Use** `review-animations`, `remove-animations` and `mobile-native`. Most prospects will be on phones. |
| **GSAP official skills** (greensock/gsap-skills) | Teaches the agent correct use of GSAP and ScrollTrigger (the scroll-animation engine). | ~18k / MIT / Jul 29, 2026 | **Use** if we build any scroll moment. Comes from the library's own makers. |
| **scroll-craft** (nateherkai/scroll-craft) | Skill for scroll-driven "immersive" sites; ships a headless-browser checker that flags dead scroll, unreadable text over video, and clips that never load. | ~5k / MIT / Sep 30, 2026 | **Maybe, only for the signature section.** Its default style leans "flashy immersive," which is the wrong tone for most of this site. |
| UI UX Pro Max (nextlevelbuilder) | Large catalog of preset styles and palettes. | ~149k / MIT | **Skip.** Preset styles are part of why sites look generated **[inference; skimmed README only]**. |
| Superdesign skill | Design agent powered by the superdesign.dev cloud service. | ~1k / MIT | **Skip.** Needs a third-party account and sends code context out. |
| Oil UI, awwwards-skill, refactoring-ui-skill | Direction explorer / orchestrator of other skills / rulebook from the *Refactoring UI* book. | 3.2k MIT / 35 MIT / 400 unlicensed | **Skip.** Overlap, too small, or unclear license for client work. |
| wilwaldon/Claude-Code-Frontend-Design-Toolkit | A curated list of the above and more. | ~1.3k / no license | **Read, don't install.** Good map of the space. |

**Recommended skill kit (5):** frontend-design → Impeccable → Emil's motion skills → GSAP skills → (scroll-craft only if the signature scroll piece is approved). Install them **into the project folder only**, pinned to a version, after reading each one's scripts. Nothing has been installed.

### 2c. Animation and scroll libraries

| Library | What it does | License | Verdict |
|---|---|---|---|
| **GSAP + ScrollTrigger** | The industry-standard animation engine; ScrollTrigger ties animation to scroll position. | Free for commercial client sites since Webflow bought it (custom "no-charge" license, May 2025). **Not open source**; the only real restriction is not building a tool that competes with Webflow **[verified]**. | **Use.** |
| **Lenis** (darkroomengineering) | Smooth-scroll library used by most award-site agencies. | MIT, ~17k stars, active | **Use lightly or not at all.** Smooth scroll feels premium on desktop but can fight phone scrolling and accessibility settings. Turn off on touch devices and for "reduce motion" users. |
| Motion (formerly Framer Motion) | React-first animation library. | MIT, ~35k | Skip unless we pick React; GSAP covers it. |
| three.js / react-three-fiber / Google model-viewer | Live 3D in the browser. | MIT / MIT / Apache-2.0 | Only if we choose a live 3D truck. Heavy on phones. |
| Theatre.js | Visual motion editor. | Apache-2.0, last update Aug 2024 | **Skip**, looks unmaintained. |

**Scroll-scrubbed video, technically** **[verified, muffinman.io]**: a normal video file only stores full frames occasionally (keyframes), so jumping around on scroll stutters. Fix is re-encoding with a keyframe every ~5-10 frames, which makes the file about 5x bigger, and serving both MP4 (iPhone) and WebM (Firefox). The more reliable approach used on Apple-style pages is an **image sequence** (one picture per frame, painted onto a canvas as you scroll). A 150-frame sequence at ~50 KB per frame is ~7.5 MB, which is too heavy for a phone on cell data, so mobile gets a shorter sequence or a still photo **[inference from standard practice]**.

### 2d. Recommended stack

| Piece | Pick | Why, in plain English | Rough cost |
|---|---|---|---|
| Framework | **Astro** | Builds plain HTML pages that load almost instantly (Google and AI search reward that), while still allowing interactive bits only where needed. Better fit than Next.js for a content/marketing site. | Free |
| Hosting | **Netlify** | Free tier allows commercial sites (Vercel's free tier does not), built-in form handling and small server functions, and Velocity Forge already has a Netlify connection. Cloudflare Pages is an equal alternative. | $0-19/mo |
| Forms + leads | **Option A: GoHighLevel** form/API → contact with source fields, auto-email + text to Anna, pipeline. **Option B:** Netlify form → email to Anna + Google Sheet. | GHL gives speed-to-lead automation and is what The Trucking School already uses (their form is a GHL/LeadConnector widget) **[verified]**. Option B is simpler but Anna works from an inbox. **Your call; see decisions.** Nothing gets changed in GHL without your explicit OK. | A: existing GHL / B: free |
| Source tracking | Capture **UTM tags** (labels on ad links saying which campaign), the Google Ads click ID, and the referring site into hidden form fields, stored for 90 days in a first-party cookie. | Every lead arrives tagged "Facebook ad / Google search / Indeed / referral". | Free |
| Analytics | **Google Analytics 4 + Search Console + Microsoft Clarity** | GA4 for traffic and conversions, Search Console for SEO, Clarity for free session recordings and heatmaps (see where people drop off). | Free |
| Call tracking (optional) | GHL numbers or CallRail | Many CDL leads call instead of filling a form; without this, those calls show as "unknown source". | ~$0-50/mo |
| Payments (optional) | **Stripe Checkout** for a **seat deposit**, not full tuition | Full tuition online drags in refunds, financing and state rules. A deposit locks the start date and is easy to refund. Stripe takes ~2.9% + 30¢ per payment. | Per transaction |
| CMS (content editor) | **None at launch.** Prices and class start dates live in one data file Claude edits. Add **Keystatic or TinaCMS** later if the client wants to edit themselves. | A CMS is a second system to maintain; the only things that change often are dates and prices. | Free |
| SEO + AI search | Structured data (code that tells Google and AI assistants "this is a school, this course costs $X, starts on Y"), a real FAQ page, the price on the page, a **Google Business Profile for the Lindon campus**, and an llms.txt file. | AI answers ("how much is CDL school near Provo?") cite pages that state the price and facts plainly. The Business Profile is the single biggest local lever. | Free |

---

## 3. Stress-test: the scroll "exploded truck" idea

### What was pitched
A Higgsfield AI video of a truck cab interior, used so that as you scroll, parts break apart and come back together, to say "we break down everything you need."

### Honest problems
1. **It breaks the client's one hard rule.** He said AI-looking sites "look stupid." AI video is the most recognizable AI artifact on the web right now. Truck cabs are a worst case: shifter patterns, gauge clusters, mirror placement, dash text and logos are things drivers, instructors and the owner will check, and current AI video tends to get small mechanical detail and text wrong **[inference]**.
2. **"Exploding" footage doesn't hold together.** An exploded view needs every part to stay the same shape as it moves. AI video generates each frame by guessing, so parts tend to melt or morph mid-move **[inference]**. You'd burn credits chasing a clean take.
3. **The metaphor is slightly off.** A CDL school doesn't teach you to take a cab apart. It does teach the **pre-trip inspection** (air brakes, coupling, lights, tires, steering), which is literally a system-by-system breakdown of the truck and part of the CDL skills test. That's the version worth building.
4. **Phones and ads.** Prospects mostly arrive from Facebook/Google ads on phones. A heavy scroll sequence slows the page, and page speed affects what Google charges per ad click **[inference]**. Scroll-jacking (taking over the scroll) also annoys people who just want the price.
5. **Cost is not the issue.** Higgsfield plans run roughly $15-84/mo; premium video models cost 40-70 credits per generation **[from a competitor's blog, unverified]**. Cheap money, expensive in time and risk.

### Production options compared

| Option | Look | Cost (rough) | Risk |
|---|---|---|---|
| AI video (Higgsfield) | Can look great in a still, wobbly in motion | $15-84/mo + many hours of retries | High: "AI look," morphing parts, brand-logo issues |
| **3D model render** (licensed truck model, exploded in Blender, exported as an image sequence) | Clean, precise, "product launch" premium | $100-500 for the model + $1.5k-5k for a 3D artist **[estimate]** | Medium: needs a good artist; avoid manufacturer logos unless it's their actual truck brand |
| Real filmed footage (your photographer, slider/gimbal walkaround of their training truck) | Most authentic | Add 2-4 hrs to the planned shoot | Low, but it can't "explode," it can only move around the truck |
| Live 3D in the browser (three.js) | Interactive, impressive on desktop | Same model cost + more dev time | Heavy on phones; needs a still fallback |

### Rating
- **As pitched: 3/10.** Strong instinct (one signature moment), wrong medium for this client.
- **Reworked: 7/10.** A 3D render of their training truck's inspection systems that separates into labeled sections as you scroll (Air brakes / Coupling / Lights / Tires / Steering), each label linking to what you learn, desktop only, with a real photo on phones.
- **What makes it a 10:** rendered from the exact model they train on; each part maps to a real pre-trip checklist item and the hours spent on it; under ~2 MB on mobile, still works with JavaScript off; ends on the price, the next start date and the request-info button; and Impeccable/scroll-craft checks pass at every scroll position.

### Three alternative signature moments (cheaper, more on-brand)
1. **The pre-trip walkaround.** A real photo of their training truck, with your photographer shooting it from ~8 angles. Scrolling walks you around the truck; inspection points light up with what students learn there. Real, teaches something, and it's the actual skills test. **My pick.**
2. **Your route to a CDL.** A scroll along a road with mile markers for each step: permit, classroom (ELDT theory), range, road, skills test, first paycheck. Each marker shows real days and dollars. Answers the top two questions (how long, how much) while looking designed, not templated.
3. **Ride-along clips.** Short real videos of instructors talking a student through a backing maneuver or a downshift, shot by your photographer. No effects. Authenticity is the premium here.

---

## 4. Design direction (pick one)

Both directions use the client's red, real photos, and one signature moment. Both avoid the AI tells listed in 2b. Fonts below are free and licensed for commercial use.

### Direction A: "Signage" (wayfinding, highway-built)
- **Idea:** the visual language of the road itself. Type set in **Overpass** (an open-source font based on the US highway-sign typeface), information laid out like route signs and mile markers, only where it carries real info (steps, dates, distances).
- **Color:** asphalt gray, reflective sign white, Centennial red as the brake-light/stop color for actions. Deliberately **not** black + red (that combination is one of the common AI defaults).
- **Photos:** wide, high-contrast shots on real Utah roads; trucks in motion.
- **Signature moment:** "Your route to a CDL" (alternative 2).
- **Risk:** can tip into theme-park kitsch if signs appear everywhere. Rule: one sign device per screen, max.

### Direction B: "Documentary" (people-first, editorial)
- **Idea:** the company's "people-first" voice made visual. Large real portraits of instructors and graduates, hands on the wheel, the pre-trip at dawn with Timpanogos behind the yard. Copy in instructors' own words.
- **Type:** a sturdy grotesque like **Archivo** (variable widths: condensed for big headlines, normal for reading), one family only.
- **Color:** daylight, warm neutrals, red used sparingly as the brand accent.
- **Signature moment:** the pre-trip walkaround (alternative 1).
- **Risk:** lives or dies on the photo shoot. Weak photos make it look like a template.

**My recommendation: B with A's route timeline used once on the Programs page.** Direction B is harder to fake and harder for a competitor to copy, it matches the parent brand's voice, and the client's photographer budget already exists. Direction A is the safer choice if the photo shoot slips past launch.

---

## 5. Page structure

### Home (in order)
1. **Hero:** one real photo, a plain headline that says what it is and where ("Get your Class A CDL in Lindon"), the price, the next start date, two buttons (Request info / Call). No slogan pairs.
2. **Proof strip:** FMCSA Training Provider Registry listing, backed by a working Utah trucking company (DBE/WBE certified), instructor-to-student ratio, Google rating, all only if true **[ask client]**.
3. **Signature moment** (walkaround or route).
4. **Programs at a glance:** Class A, Class B, refreshers, endorsements, each with price, length and schedule.
5. **What happens after:** the job path (does Centennial hire grads? local construction hauling means home every night, a real differentiator vs. long-haul).
6. **Instructors:** names, faces, years driving.
7. **Cost and funding:** what's included, payment plans, Workforce Services / WIOA (federal job-training money), veterans' benefits **[ask client]**.
8. **Graduate stories:** named, with photos, from Google reviews.
9. **FAQ** (top 6, links to full FAQ).
10. **Request-info form** + phone + address + map.

### Key pages
- **Programs & pricing:** one section per program: price, what's included, hours/weeks, schedule, requirements (age, medical card, permit), next starts. Route-to-CDL timeline lives here.
- **Schedule:** upcoming class start dates, day/evening options, seats left. Fed from one data file.
- **Financing:** payment plans, Workforce Services, veterans, employer sponsorship, a seat deposit option.
- **About & instructors:** the Centennial connection, the yard and trucks, instructor bios, safety record.
- **FAQ:** cost, length, age, DOT physical, permit, pass rates, what if I fail, job placement, ELDT and the registry, Spanish-language options **[ask client]**. Marked up for Google/AI answers.
- **Apply / Request info:** short form (name, phone, email, program, preferred start, how did you hear) plus hidden source tracking; optional deposit checkout.
- Also: privacy policy, refund policy (required if taking payments), thank-you page (needed to count conversions).

---

## 6. Decisions Jayce needs to make before the wireframe

1. **Direction:** A (Signage), B (Documentary), or B + A's route timeline (my recommendation).
2. **Signature moment:** pre-trip walkaround (my pick, photo-based, cheap), route timeline, or the reworked 3D exploded truck (adds ~$2-5k and a 3D artist; would need client buy-in on budget).
3. **Lead backend:** GoHighLevel (speed-to-lead automation, recurring Velocity Forge service) vs. a simple email-plus-sheet form. This also decides whether "pay and sign up" is a GHL payment link or Stripe.

## 7. Questions to send the client before or with the wireframe
(Not sent. For Jayce to choose.)
- School name, Lindon address, and whether it's on the FMCSA Training Provider Registry (required since Feb 2022 for entry-level training; only listed providers can train first-time Class A/B drivers **[verified, FMCSA FAQ]**).
- Programs, prices, length, schedule, what's included, and how "below market" is defined (vs. The Trucking School $4,400 or MTECH $1,820).
- Funding: Workforce Services approved? payment plans? Does Centennial hire graduates or reimburse tuition?
- Brand file (logo, exact red, fonts) and photo rights for existing images.
- Who gets leads besides Anna, and how fast can Anna call back.

## 8. Things I could not do or check
- Read Jayce's "AI Brain" file in Google Drive: the read was blocked by this session's permission check, so this report doesn't reflect its rules.
- Exact brand colors/fonts from centennialtrucking.com (text-only page reader).
- The Optikka/Codrops case study on scroll sequences (page failed to load).
- Higgsfield pricing from Higgsfield itself (only a competitor's blog).

## Sources
- centennialtrucking.com: home, about, careers, contact, services, construction trucking, notable jobs, service areas (read Nov 12, 2026)
- MTECH CDL: https://mtec.edu/programs/commercial-drivers-license and https://catalog.mtec.edu/programs/iQniaoL4BfvB4lqbWwz0/cost-qLAEy
- The Trucking School: https://the-trucking-school.com/training
- FMCSA Training Provider Registry FAQ: https://tpr.fmcsa.dot.gov/FAQ/Topics/provider-requirements
- GSAP license: https://webflow.com/blog/gsap-becomes-free and https://gsap.com/community/standard-license/
- Video scrubbing: https://muffinman.io/blog/scrubbing-videos-using-javascript/
- Higgsfield pricing (competitor blog, unverified): https://creatify.ai/blog/higgsfield-pricing-(2026)-plans-and-what-you-ll-actually-pay
- Utah CDL school directory: https://resumegeni.com/blog/cdl-schools-utah
- GitHub READMEs (raw, read Nov 12, 2026): pbakaus/impeccable, anthropics/skills (frontend-design), Nutlope/hallmark, Leonxlnx/taste-skill, emilkowalski/skills, greensock/gsap-skills, nateherkai/scroll-craft, nextlevelbuilder/ui-ux-pro-max-skill, superdesigndev/superdesign-skill, oil-oil/oil-ui, Ga14ctic/awwwards-skill, edisonmbli/refactoring-ui-skill, wilwaldon/Claude-Code-Frontend-Design-Toolkit. Star counts and licenses from the GitHub search API.
