# Anti-AI Slop: The Unified Field Guide

A single reference for detecting and removing AI-generated slop from any creative output: visual design, interfaces, text, and prose.

## What's in it

AI slop is the same problem in two domains. LLMs and diffusion models produce the **most statistically likely output**, the centroid of their training distribution. In visual design, that means certain color palettes, layout patterns, and component choices. In text, it means certain phrases, structures, and tonal patterns. Both are detectable. Both are fixable.

This guide covers both:

**Domain I: Visual and Aesthetic Slop**
- 6 absolute bans (side-stripe borders, gradient text, glassmorphism, hero-metric template, identical card grids, modal-as-first-thought)
- AI color palette tells by domain (Tech/SaaS, Healthcare, Finance, Crypto, AI/ML)
- Typography, layout, and motion tells
- Two-altitude category-reflex check
- Automated detection via `npx impeccable detect`

**Domain II: Text and Writing Slop**
- 12-tell quick scan (catches ~80% of AI text in 60 seconds)
- Full 29-pattern reference with before/after examples
- Voice injection guide: how to write like a human, not just avoid patterns

Plus a unified three-phase audit process for any creative output.

## Usage

This is a [Hermes Agent](https://hermes-agent.nousresearch.com) skill. Drop `SKILL.md` into your skills directory:

```bash
cp SKILL.md ~/.hermes/profiles/default/skills/anti-ai-slop/
```

Then invoke it with any of these triggers:
- "audit this for AI slop"
- "de-slop this landing page"
- "humanize this text"
- "anti-AI pass on this document"
- "make this not look AI-generated"

It also works as a standalone reference. The patterns are tool-agnostic.

## Automated Detection

For visual slop, run the deterministic detector (no LLM, no API key, 27 rules):

```bash
npx impeccable detect src/
npx impeccable detect index.html
npx impeccable detect https://example.com
```

## Attribution

This guide synthesizes two open-source projects:

- **Visual slop patterns:** [pbakaus/impeccable](https://github.com/pbakaus/impeccable) (Apache 2.0)
- **Text slop patterns:** [blader/humanizer](https://github.com/blader/humanizer) (MIT), based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)

## License

The visual slop patterns (Domain I) are Apache 2.0. The text slop patterns (Domain II) are MIT. The synthesis and unified framework are MIT. See [LICENSE](LICENSE) for full terms.
