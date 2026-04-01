# Action Backend Spec

This file defines the intended backend behavior if you use a **Custom GPT Action** to score the diagnostic while keeping the UX inside ChatGPT.

## Why This Exists

You asked whether this could be done through APIs while still living behind a ChatGPT GPT link.

Current product boundary as of **March 31, 2026**:

- **Yes**: you can create a Custom GPT in ChatGPT and attach your own API through an Action.
- **No**: you cannot create the ChatGPT-hosted GPT page itself through the OpenAI API alone.

So the viable architecture is:

1. Build the GPT in ChatGPT
2. Paste in `custom-gpt-instructions.md`
3. Upload knowledge files if needed
4. Add an Action using `openapi.yaml`
5. Host your own endpoint that scores the diagnostic

## Recommended Backend Responsibilities

Your backend should:

- accept the user's answers,
- normalize them into scoring dimensions,
- choose exactly one archetype,
- return the matching card content,
- return the shadow form,
- return compatibility guidance,
- return three next moves.

The GPT should remain responsible for:

- asking questions conversationally,
- deciding when it has enough information,
- passing the answer set to the Action,
- and presenting the returned result cleanly.

## Minimal Endpoint

`POST /v1/diagnostic/score`

Input:

- optional subject metadata
- list of question/answer pairs
- optional scoring overrides if you later want manual tuning

Output:

- `archetype`
- `confidence`
- `tagline`
- `definition`
- `ascii_avatar`
- `signature_abilities`
- `why_this_fits`
- `core_leverage`
- `best_fit_contexts`
- `shadow_form`
- `works_well_with`
- `friction_risks`
- `pendulum_read`
- `next_moves`

## Suggested Implementation Notes

- Keep scoring deterministic and auditable
- Return exactly one archetype
- Do not return a secondary archetype
- If the score is mixed, lower confidence and reflect ambiguity in `why_this_fits`
- Keep card copy stable so the archetypes become recognizable over time
- Keep shadow copy sharp but professional

## Good First Version

For v1, you do not need ML or embeddings.

A simple rules engine is enough:

- assign per-answer weights to each dimension,
- aggregate dimension totals,
- map dimension profiles to archetype scores,
- apply tie-break rules,
- choose the top result,
- generate the output payload from the fixed card library.

## When To Use This

Use the Action-backed model if you want:

- analytics,
- versioned scoring logic,
- easier iteration without editing GPT instructions every time,
- integration with your own database or admin tools.

Skip the Action if you just want:

- a fast Custom GPT,
- no backend hosting,
- and all scoring done inside the prompt.
