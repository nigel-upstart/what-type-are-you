# Engineering Leadership Archetype Diagnostic

This repository contains a Custom GPT-ready diagnostic for answering:

**"What type of engineering leader am I right now?"**

It is designed to feel more like a sharp archetype system than a generic leadership quiz:

- one current-state archetype, not a permanent identity label
- vivid character-card presentation
- ASCII avatar for each archetype
- shadow or difficult-mode interpretation
- collaboration and friction guidance
- optional archetype portrait generation

## What This Produces

The diagnostic classifies a user into one of eight leadership archetypes:

- `Guide`
- `Operator`
- `Driver`
- `Catalyst`
- `Builder`
- `Steward`
- `Mentor`
- `Strategist`

It then returns:

- a single winner by score
- confidence
- a character card with tagline and abilities
- a shadow form
- best-fit contexts
- collaboration guidance
- practical next moves

## Repo Structure

- [custom-gpt-instructions.md](custom-gpt-instructions.md)
  Paste-ready instructions for the ChatGPT GPT editor
- [archetype-cards.md](archetype-cards.md)
  Source-of-truth archetype definitions, ASCII avatars, shadow forms, and compatibility guidance
- [diagnostic-spec.md](diagnostic-spec.md)
  Question flow, scoring logic, tie-break rules, and acceptance scenarios
- [openapi.yaml](openapi.yaml)
  Optional Custom GPT Action schema for API-backed scoring
- [action-backend-spec.md](action-backend-spec.md)
  Backend contract for the hybrid ChatGPT-plus-API path
- [CLAUDE.md](CLAUDE.md)
  Repo guidance for future edits

## How To Use

### Custom GPT only

1. Open the GPT editor in ChatGPT.
2. Paste [custom-gpt-instructions.md](custom-gpt-instructions.md) into the `Instructions` field.
3. Upload:
   - [archetype-cards.md](archetype-cards.md)
   - [diagnostic-spec.md](diagnostic-spec.md)
4. Enable `Image Generation` if you want archetype portraits.
5. Leave the other capabilities off unless you need them.

### Custom GPT plus API

If you want analytics, versioned scoring logic, or a backend-owned rules engine:

1. Build a backend that implements [action-backend-spec.md](action-backend-spec.md)
2. Add an Action in the GPT editor using [openapi.yaml](openapi.yaml)
3. Keep the same knowledge files and prompt

## Product Boundary

As of March 31, 2026:

- ChatGPT-hosted GPTs are created in the GPT Builder
- OpenAI API assistants are hosted by you

If you want a shareable ChatGPT link, the right deployment target is a **Custom GPT**.

If you want API-backed scoring while keeping the UX in ChatGPT, use a **Custom GPT Action**.

## Design Notes

The model is built around four core dimensions:

- `People & Culture`
- `Execution & Results`
- `Change & Innovation`
- `Stability & Process`

The interview is intentionally conversational:

- 8 to 10 questions
- one at a time
- `A/B/C/D` or freeform answers
- internal scoring
- targeted tie-breakers only when needed

The tone target is:

- sharp
- practical
- engineering-specific
- slightly game-like
- credible enough for real leadership reflection
