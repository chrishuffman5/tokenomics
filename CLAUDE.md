# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file HTML slide deck on **LLM tokenomics** — what tokens are, how input/output billing works, prompt caching, context bloat from skills/MCP/history, and Amazon Bedrock as the worked pricing example. Built to be presented in ~15 minutes.

There is no build system, no package manager, no tests. The deliverable is `index.html`, fully self-contained (inline CSS + JS, no external assets, no fonts loaded over the network).

## Running it

Open `index.html` directly in a browser. No server needed.

- Navigation: arrow keys / space / page up-down / home / end, click left or right half of the screen, or swipe on touch devices.
- Deep-linking: `index.html#7` jumps to slide 7. The current slide number is mirrored to `location.hash`.
- Print to PDF: the `@media print` block expands every slide to a full page and hides chrome. Use the browser's "Save as PDF" with default margins.

## Editing slides

Each slide is a `<section class="slide">` inside `<div class="deck">`. The first slide gets `class="slide active"`; the navigator manages `.active` after that. Slide count in the footer is read from the DOM, so adding or removing a `<section>` just works — no counter to update.

When adding a slide, keep the title-slide special case in mind: that one uses `class="slide title-slide"` and a centered layout. Other slides default to a left-aligned column layout via `.slide`.

## Pricing numbers in the deck

The Bedrock pricing examples (Claude Sonnet 4.6: $3 input / $15 output / $3.75 5-min cache write / $0.30 cache read per 1M tokens; $6.00 1-hour cache write; batch 50% off) were taken from `https://aws.amazon.com/bedrock/pricing/`. Bedrock pricing changes — newer models arrive, older ones move to "extended access" tiers. Before re-presenting, re-verify the rates on the live page and update slide 7 (the pricing table) and the worked examples (slides 10–12, 14) so the math stays internally consistent.

The compounding-cost table on slide 14 uses the same input rate. If you change the input rate, recompute that whole column.

## Design tokens

Colors and most sizing live in CSS custom properties at `:root` and a `prefers-color-scheme: light` override. Theme-wide changes should be made there rather than per-element. Slide-content typography uses `clamp(...)` so the deck scales reasonably from a 13" laptop to a projector without media queries.
