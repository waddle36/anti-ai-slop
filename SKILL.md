---
name: anti-ai-slop
description: "Unified field guide for detecting and removing AI-generated slop from any creative output: visual design, interfaces, text, prose, and writing. Use when the user wants to audit, de-slop, humanize, or harden anything against the AI 'look' or 'sound'. Covers both frontend/visual slop (color palette tells, layout patterns, component choices, typography, motion) and text/prose slop (29 writing patterns, voice injection, filler removal). Triggered by: 'de-slop', 'anti-AI pass', 'make this not look AI-generated', 'humanize this', 'audit for AI tells', or any quality pass before shipping creative work."
version: 1.0.0
license: MIT (humanizer patterns from blader/humanizer v2.5.1), Apache 2.0 (impeccable patterns from pbakaus/impeccable)
metadata:
  hermes:
    tags: [anti-ai-slop, design, writing, humanize, quality, audit, de-slop]
    category: creative
    supersedes: [impeccable, humanizer]
---

# Anti-AI Slop: The Unified Field Guide

AI-generated slop is the same problem in two domains. LLMs and diffusion models produce the **most statistically likely output**: the centroid of their training distribution. In visual design, that's certain color palettes, layout patterns, and component choices. In text, it's certain phrases, structures, and tonal patterns. Both are detectable. Both are fixable.

This skill covers both domains as a single framework.

---

## The Unified Principle

> AI does not make choices. It pattern-matches to the nearest cluster center.

The slop test for any output, visual or textual, is: **could someone look at this and say "AI made that" without doubt?** If yes, it failed.

Two altitudes matter:

1. **First-order**: the obvious category reflex. Healthcare → white + teal. Tech blog → "delves into" and "in today's rapidly evolving landscape." This is what everyone catches.
2. **Second-order**: the trap one tier deeper. You avoided the first reflex, but landed in the second most common aesthetic lane. The output still reads as "AI that tried to not look like AI."

Both domains share the same root failures:
- **Over-emphasis**: puffing up importance with ceremonial language or decorative elements
- **Uniformity**: every paragraph/card/section has identical rhythm and structure
- **Hedging**: refusing to commit to a specific choice
- **Template capture**: the output fits a common template so perfectly it's invisible to the creator

---

## Domain I: Visual & Aesthetic Slop

Covers websites, landing pages, dashboards, app UI, components, slides, documents, and any visual frontend. Based on [impeccable](https://github.com/pbakaus/impeccable).

### Absolute Bans (rewrite the element if you see these)

| Pattern | Why It's Slop | Fix |
|---------|---------------|-----|
| **Side-stripe borders** | `border-left: 3px solid accent` on cards, list items, callouts | Full borders, background tints, leading numbers, or nothing |
| **Gradient text** | `background-clip: text` with gradient: decorative, never meaningful | Single solid color. Emphasis via weight or size |
| **Glassmorphism as default** | Blurred glass cards used decoratively | Rare and purposeful, or nothing |
| **Hero-metric template** | Big number + small label + supporting stats + gradient accent | Typographic heroes, narrative layouts, or data in cards |
| **Identical card grids** | Same-sized cards with icon + heading + text, repeated | Vary at least one dimension. Make one full-width. Change structure |
| **Modal as first thought** | Modal for everything instead of inline/progressive disclosure | Inline expansion, slide-outs, accordions, or progressive disclosure |

### AI Color Palette Tells

These palettes appear because they're overrepresented in training data:

| Domain | AI Default | The Fix |
|--------|-----------|---------|
| Tech/SaaS | Dark blue + purple gradient | Choose the palette from the physical scene, not the category |
| Healthcare | White + teal + blue | Linen + committed green reads as quiet luxury, not clinical |
| Finance | Navy + gold | Terminal-native dark, editorial warm neutrals, something unexpected |
| Crypto/Web3 | Neon on black | Restrained typographic treatment with one committed accent |
| AI/ML product | Purple-to-cyan gradient, dark mode | Pick one. Commit to it. Don't gradient between them |

**Color strategy framework:**
- **Restrained**: tinted neutrals + one accent ≤10%. Product default.
- **Committed**: one saturated color carries 30-60% of surface. Brand default.
- **Full palette**: 3-4 named roles, each deliberate. Campaigns, data viz.
- **Drenched**: the surface IS the color. Brand heroes.

Use OKLCH. Reduce chroma as lightness approaches 0 or 100. Never `#000` or `#fff`: tint every neutral toward the brand hue.

### Typography Tells

- **Overused fonts:** Inter, Space Grotesk, Plus Jakarta Sans, Satoshi, Switzer: these scream "2024 AI design"
- **Single-font pages**: no contrast between headings and body
- **Flat hierarchy**: less than 1.25x ratio between typographic steps
- **Italic-serif-display headlines**: Playfair/Georgia italic for hero text is the #1 AI slop font pairing
- **Body text at viewport edge**: cap at 65-75ch
- **All-caps body text, wide tracking**: unreadable and mechanical

### Layout Tells

- **Monotonous spacing**: identical padding everywhere reads as algorithmic
- **Everything centered**: centering is a default, not a choice
- **Nested cards**: cards inside cards. Always wrong.
- **Everything in a container**: most things don't need one
- **Wrapping nothing**: body text hitting full viewport width

### Motion Tells

- **Bounce easing**: instant AI tell. Use ease-out-quart/quint/expo
- **Dark-glow**: box-shadows with colored glow on dark backgrounds
- **Animating layout properties**: `height`, `width`, `top`, `left`. Use `transform` and `opacity`

### The Category-Reflex Check (Visual)

Before finalizing any design, run two questions:

1. **First-order:** Could someone guess the theme + palette from the category alone? ("Observability → dark blue", "Healthcare → white + teal")
2. **Second-order:** Could someone guess the aesthetic family from category-plus-anti-references? ("AI workflow tool that's not SaaS-cream → editorial-typographic")

If either answer is obvious, rework the physical scene sentence and color strategy.

### Automated Detection

Run the deterministic anti-pattern detector (no LLM, no API key: 27 rules):

```bash
npx impeccable detect src/                   # scan a directory
npx impeccable detect index.html             # scan a file
npx impeccable detect https://example.com    # scan a URL
npx impeccable detect --fast --json .        # regex-only, JSON output
```

---

## Domain II: Text & Writing Slop

Covers prose, blog posts, essays, documentation, emails, social media, PR descriptions, resumes, and any text output. Based on [blader/humanizer](https://github.com/blader/humanizer) v2.5.1 and Wikipedia's WikiProject AI Cleanup.

### Quick Scan: The 12 Most Reliable Tells

If you only have 60 seconds, check for these. They catch ~80% of AI text:

1. **Em dashes** (—) used more than once per ~500 words
2. **"Delve"** anywhere in the text
3. **"In today's rapidly evolving [X] landscape"** or variants
4. **"It's not just about X; it's about Y"** (negative parallelism)
5. **"Additionally," / "Moreover," / "Furthermore,"** at paragraph starts
6. **Bold-faced keywords** followed by colons in lists (inline-header pattern)
7. **"-ing" sentence tails** ("underscoring its importance", "highlighting the need for")
8. **Vague attributions** ("Industry observers have noted", "Experts argue", "Some critics say")
9. **"Serves as a testament to"** or any copula avoidance ("serves as", "stands as", "functions as")
10. **"I hope this helps!" / "Let me know if..."** (chatbot artifacts)
11. **Generic positive conclusions** ("The future looks bright", "Exciting times lie ahead")
12. **Rule of three** applied mechanically to every list

### Full Pattern Reference (29 patterns)

#### CONTENT PATTERNS

**1. Significance Inflation**
Words: *stands/serves as, testament/reminder, vital/significant/crucial/pivotal/key role/moment, underscores/highlights its importance, reflects broader, marking/shaping the, indelible mark*

Before: "The institute was established in 1989, marking a pivotal moment in the evolution of regional statistics."
After: "The institute was established in 1989 to collect and publish regional statistics."

**2. Notability Overemphasis**
Words: *independent coverage, local/regional/national media outlets, written by a leading expert, active social media presence*

Before: "Her views have been cited in The New York Times, BBC, Financial Times."
After: "In a 2024 New York Times interview, she argued that AI regulation should focus on outcomes."

**3. Superficial -ing Endings**
Words: *highlighting/underscoring/emphasizing..., ensuring..., reflecting/symbolizing..., contributing to..., cultivating/fostering..., showcasing...*

Before: "The palette resonates with natural beauty, symbolizing Texas bluebonnets, reflecting the community's connection to the land."
After: "The architect said the colors reference local bluebonnets and the Gulf coast."

**4. Promotional/Advertisement Language**
Words: *boasts a, vibrant, rich (figurative), profound, nestled, in the heart of, breathtaking, must-visit, stunning*

Before: "Nestled within the breathtaking region, it stands as a vibrant town with rich cultural heritage."
After: "The town is known for its weekly market and 18th-century church."

**5. Vague Attributions (Weasel Words)**
Words: *Industry reports, Observers have cited, Experts argue, Some critics argue, several sources/publications*

Before: "Experts believe it plays a crucial role in the regional ecosystem."
After: "It supports several endemic fish species, according to a 2019 survey by the Chinese Academy of Sciences."

**6. Formulaic "Challenges and Future Prospects" Sections**
Words: *Despite its..., faces several challenges..., Despite these challenges, Future Outlook*

Before: "Despite its prosperity, it faces challenges typical of urban areas. Despite these challenges, it continues to thrive."
After: "Traffic increased after 2015 when three new IT parks opened. A drainage project began in 2022."

#### LANGUAGE PATTERNS

**7. Overused AI Vocabulary**
High-frequency words: *actually, additionally, align with, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight, interplay, intricate/intricacies, key, landscape (abstract), pivotal, showcase, tapestry (abstract), testament, underscore, valuable, vibrant*

Before: "An enduring testament to colonial influence is the widespread adoption of pasta, showcasing how dishes integrated into the landscape."
After: "Pasta dishes, introduced during colonization, remain common in the south."

**8. Copula Avoidance**
Words: *serves as/stands as/marks/represents [a], boasts/features/offers [a]*

Before: "Gallery 825 serves as LAAA's exhibition space and boasts over 3,000 square feet."
After: "Gallery 825 is LAAA's exhibition space. It has four rooms totaling 3,000 square feet."

**9. Negative Parallelisms and Tailing Negations**
Before: "It's not just about the beat; it's part of the aggression. It's not merely a song, it's a statement."
After: "The heavy beat adds to the aggressive tone."

Before (tailing negation): "The options come from the selected item, no guessing."
After: "The options come from the selected item without forcing the user to guess."

**10. Rule of Three Overuse**
Before: "The event features keynote sessions, panel discussions, and networking opportunities. Attendees can expect innovation, inspiration, and industry insights."
After: "The event includes talks and panels. There's also informal networking between sessions."

**11. Elegant Variation (Synonym Cycling)**
Before: "The protagonist faces challenges. The main character must overcome obstacles. The central figure triumphs."
After: "The protagonist faces many challenges but eventually triumphs."

**12. False Ranges**
Before: "From the singularity of the Big Bang to the grand cosmic web, from the birth of stars to the dance of dark matter."
After: "The book covers the Big Bang, star formation, and current dark matter theories."

**13. Passive Voice and Subjectless Fragments**
Before: "No configuration file needed. The results are preserved automatically."
After: "You do not need a configuration file. The system preserves the results automatically."

#### STYLE PATTERNS

**14. Em Dash Overuse**
Before: "The term is promoted by Dutch institutions—not by the people themselves. You don't say 'Netherlands, Europe' as an address—yet this continues—even officially."
After: "The term is promoted by Dutch institutions, not by the people themselves. You don't say 'Netherlands, Europe' as an address, yet this continues in official documents."

**15. Boldface Overuse**
Before: "It blends **OKRs**, **KPIs**, and visual tools such as the **Business Model Canvas** and **Balanced Scorecard**."
After: "It blends OKRs, KPIs, and visual strategy tools like the Business Model Canvas and Balanced Scorecard."

**16. Inline-Header Vertical Lists**
Before: "- **User Experience:** The interface has been improved.\n- **Performance:** Algorithms are optimized.\n- **Security:** Encryption is added."
After: "The update improves the interface, speeds up load times, and adds end-to-end encryption."

**17. Title Case in Headings**
Before: "## Strategic Negotiations And Global Partnerships"
After: "## Strategic negotiations and global partnerships"

**18. Emojis as Structural Decoration**
Before: "🚀 **Launch Phase:** The product launches in Q3\n💡 **Key Insight:** Users prefer simplicity"
After: "The product launches in Q3. User research showed a preference for simplicity."

**19. Curly Quotation Marks**
Before: "He said \u201cthe project is on track\u201d but others disagreed."
After: "He said \"the project is on track\" but others disagreed."

#### COMMUNICATION PATTERNS

**20. Chatbot Correspondence Artifacts**
Words: *I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., let me know, here is a...*

Before: "Here is an overview of the French Revolution. I hope this helps! Let me know if you'd like me to expand."
After: "The French Revolution began in 1789 when financial crisis and food shortages led to widespread unrest."

**21. Knowledge-Cutoff Disclaimers**
Words: *as of [date], Up to my last training update, While specific details are limited/scarce..., based on available information...*

Before: "While specific details are not extensively documented in readily available sources, it appears to have been established in the 1990s."
After: "The company was founded in 1994, according to its registration documents."

**22. Sycophantic/Servile Tone**
Before: "Great question! You're absolutely right that this is a complex topic. That's an excellent point."
After: "The economic factors you mentioned are relevant here."

#### FILLER AND HEDGING

**23. Filler Phrases**
- "In order to achieve this goal" → "To achieve this"
- "Due to the fact that" → "Because"
- "At this point in time" → "Now"
- "In the event that" → "If"
- "The system has the ability to" → "The system can"
- "It is important to note that" → (delete)

**24. Excessive Hedging**
Before: "It could potentially possibly be argued that the policy might have some effect."
After: "The policy may affect outcomes."

**25. Generic Positive Conclusions**
Before: "The future looks bright. Exciting times lie ahead as they continue their journey toward excellence."
After: "The company plans to open two more locations next year."

**26. Hyphenated Word Pair Overuse**
Watch for: *third-party, cross-functional, client-facing, data-driven, decision-making, well-known, high-quality, real-time, long-term, end-to-end*

Before: "The cross-functional team delivered a high-quality, data-driven report."
After: "The cross functional team delivered a high quality, data driven report."

**27. Persuasive Authority Tropes**
Phrases: *The real question is, at its core, in reality, what really matters, fundamentally, the deeper issue, the heart of the matter*

Before: "The real question is whether teams can adapt. At its core, what really matters is organizational readiness."
After: "The question is whether teams can adapt. That mostly depends on whether the organization is ready to change its habits."

**28. Signposting and Announcements**
Phrases: *Let's dive in, let's explore, let's break this down, here's what you need to know, now let's look at, without further ado*

Before: "Let's dive into how caching works in Next.js. Here's what you need to know."
After: "Next.js caches data at multiple layers, including request memoization, the data cache, and the router cache."

**29. Fragmented Headers**
Before:
> ## Performance
>
> Speed matters.
>
> When users hit a slow page, they leave.
After:
> ## Performance
>
> When users hit a slow page, they leave.

### Adding Voice (Beyond Just Removing Patterns)

Sterile, voiceless writing is just as obvious as slop. Good writing has a human behind it:

- **Have opinions.** Don't just report facts: react to them
- **Vary rhythm.** Short punchy sentences. Then longer ones that take their time
- **Acknowledge complexity.** "This is impressive but also kind of unsettling"
- **Use "I" when it fits.** First person isn't unprofessional: it's honest
- **Let some mess in.** Perfect structure feels algorithmic
- **Be specific about feelings.** Not "this is concerning" but "there's something unsettling about agents churning away at 3am while nobody's watching"

---

## The Unified Audit Process

When asked to audit anything for AI slop:

### Phase 1: Visual Audit
1. Run `npx impeccable detect` on the frontend/directory
2. Check against the 6 absolute bans
3. Verify color palette: does the category predict it?
4. Check typography: overused fonts? Flat hierarchy?
5. Run the category-reflex check at both altitudes
6. Note every violation with file location

### Phase 2: Text Audit
1. Scan for the 12 quick tells (em dashes, "delve", "landscape", etc.)
2. Read the full text against all 29 patterns
3. Check for communication artifacts (chatbot language, disclaimers)
4. Evaluate voice: is there a human behind this or is it sterile?
5. Note every violation with line reference

### Phase 3: Fix
1. Rewrite/rework every flagged element
2. One more pass: what still reads as AI-generated?
3. Final polish pass

### Compressed Workflow (for pieces under ~600 words)
1. Identify tells inline as you rewrite
2. Produce the rewrite directly
3. List the tells found and fixed in a brief section
4. One final scan

---

## Attribution

This meta-skill synthesizes two open-source projects:

- **Visual slop patterns** from [pbakaus/impeccable](https://github.com/pbakaus/impeccable) (Apache 2.0): the 6 absolute bans, category-reflex framework, color strategy, and `npx impeccable detect` CLI
- **Text slop patterns** from [blader/humanizer](https://github.com/blader/humanizer) (MIT) v2.5.1: the 29 writing patterns, personality/soul injection, and voice calibration workflow
- Humanizer is itself based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained by WikiProject AI Cleanup

Original humanizer author: Siqi Chen ([@blader](https://github.com/blader)). Original impeccable author: Paul Bakaus ([@pbakaus](https://github.com/pbakaus)).
