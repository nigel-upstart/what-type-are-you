# CLAUDE.md

## Project

This repository packages a ChatGPT Custom GPT diagnostic for engineering leadership archetypes.

The core deliverables are:

- `custom-gpt-instructions.md`: paste-ready instructions for the GPT editor
- `archetype-cards.md`: canonical archetype definitions, ASCII avatars, shadow modes, and compatibility guidance
- `diagnostic-spec.md`: question flow, scoring logic, tie-break rules, and acceptance scenarios
- `openapi.yaml`: optional Custom GPT Action schema for API-backed scoring
- `action-backend-spec.md`: backend contract for the hybrid ChatGPT-plus-API path

## Intent

The product is a leadership diagnostic that:

- classifies a user's current operating mode, not fixed identity
- returns one archetype only
- presents the result as a vivid character card
- includes a shadow mode and collaboration guidance
- can optionally generate an archetype portrait

## Editing Guidelines

- Keep the Custom GPT instructions under the editor limit.
- Put richer reference material in the knowledge files, not the main instructions field.
- Preserve the single-winner classification rule.
- Keep the interview sequential: one question at a time, with optional tie-breakers.
- Keep the tone sharp and specific, not generic leadership-framework language.
- Treat image generation as optional and post-diagnosis by default.

## Style

- Favor concise, direct language.
- Keep archetype copy memorable but credible.
- Avoid HR-speak, personality-test framing, and overexplaining.
- Prefer ASCII-only art in `archetype-cards.md` unless there is a strong reason not to.

## Publishing Notes

- The primary deployment target is a ChatGPT Custom GPT.
- If API-backed scoring is needed, use a Custom GPT Action rather than a separate hosted chat UI.
- Knowledge uploads should usually include at least:
  - `archetype-cards.md`
  - `diagnostic-spec.md`

