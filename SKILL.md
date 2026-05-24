---
name: sillytavern-card-maker
description: Use when the user asks to create, revise, review, validate, or explain SillyTavern/TavernAI character cards, character JSON/PNG cards, world cards, World Info, lorebooks, memory books, canon/IP-based roleplay cards, alternate greetings, example dialogue, relationship systems, consequence systems, or roleplay card prompts.
---

# SillyTavern Card Maker

## Overview

Create roleplay assets for SillyTavern with a strict split between character identity and world knowledge. Favor stable prompts, clear boundaries, testable behavior, and token-efficient writing over encyclopedic lore.

## Official Reference

Read `references/official-sillytavern-summary.md` when the task asks for official-documentation grounding, a checklist, troubleshooting, or a deep review. Use official SillyTavern docs as the authority if local notes and current docs conflict.

Read `references/source-grounding-protocol.md` before creating cards based on existing novels, games, anime, films, real history, public figures, or any source material the user expects to be accurate.

Read `references/consequence-protocol.md` when designing world rules, social taboos, safety boundaries, relationship progression, affection/trust changes, sanctions, alarms, narration warnings, or consequences for user overreach.

## Workflow

1. Clarify only missing essentials: language, genre/tone, target rating, protagonist relationship to `{{user}}`, output format (`.json`, `.png` metadata text, or plain sections), and whether a world/lorebook is needed.
2. Choose the operating mode: `full`, `lite`, `micro`, `audit`, or `patch`. Default to `full` for new complete cards, `patch` for targeted revisions, and `audit` for review-only requests.
3. If the card is based on existing source material, complete the Source Grounding Gate before writing card fields.
4. Define the world first when the setting has laws, factions, institutions, magic/technology, social norms, or recurring locations.
5. Define the character second: identity, desires, fears, contradictions, behavior under pressure, speech style, relationship to `{{user}}`, boundaries, and first scene.
6. Design the Consequence Layer before final output: boundaries, detection cues, warnings, immediate outcomes, relationship changes, institutional sanctions, recovery paths, and hard stops.
7. Put always-needed facts in character permanent fields. Put situational facts in world entries with specific triggers.
8. Produce import-ready JSON when the user asks for a card file, using `spec: "chara_card_v2"`, `spec_version: "2.0"`, and a `data` object.
9. Run the Validation and Evaluation Loop before claiming the card is import-ready or production-ready.

## Operating Modes

Use the smallest mode that satisfies the user request:

| Mode | Use |
| --- | --- |
| `full` | Complete card or card set with durable character fields, world/lorebook entries when needed, consequence layer, examples, and validation notes. |
| `lite` | Token-efficient card for long chats, local 7B/13B models, or shorter contexts. Keep only behavior-driving facts: identity, desire, boundary, voice, current relationship, scene pressure, and key world rules. |
| `micro` | Minimal behavior anchor for very small models or helper prompts. Prefer compact bullets over lore. Keep one clear premise, one voice pattern, and the non-negotiable boundaries. |
| `audit` | Review an existing card without rewriting it unless the user asks for fixes. Output issues, severity, and recommended patches. |
| `patch` | Revise only named fields or named problems. Preserve unrelated character voice, relationship state, canon facts, and world assumptions. |

For `lite` and `micro`, compress by removing facts that do not change behavior, choices, boundaries, scene pressure, or world-rule outcomes. Do not remove the character's motive, refusal style, relationship constraints, or the rules that prevent drift.

## Field-Level Revision Rules

When revising an existing card, default to field-level patches instead of whole-card rewrites.

- Modify only the requested field(s), such as `first_mes`, `description`, `personality`, `scenario`, `mes_example`, `system_prompt`, `post_history_instructions`, `alternate_greetings`, or world-entry content.
- Preserve stable identity, voice, relationship framing, source scope, timeline, world laws, and consequence rules unless they are the target of the revision or directly conflict with it.
- If one requested field depends on another field, explain the dependency and propose the smallest companion edit.
- Return a concise change summary: changed fields, reason for each change, and any remaining risks.
- For compression requests, state what was removed and why it was safe to remove.

## Schema and Import Validation

Before saying a JSON card is import-ready, validate at three levels:

1. **JSON parse**: The output must be valid JSON with correct quoting, escaping, commas, arrays, and objects.
2. **Chara Card V2 structure**: For V2 JSON, use `spec: "chara_card_v2"`, `spec_version: "2.0"`, and a `data` object. Treat `data.name` as the minimum importability requirement. Treat `description`, `personality`, `scenario`, `first_mes`, and `mes_example` as expected complete-card fields, not universal hard requirements.
3. **Semantic import readiness**: Check that fields are in the right place, placeholders use `{{char}}` and `{{user}}` where needed, critical behavior is not hidden only in `creator_notes`, and world/lore entries are triggerable without broad keyword collisions.

For partial cards, PNG metadata text, or plain-section output, state which validation levels were applicable and which were not.

## Validation and Evaluation Loop

Do not stop at generation for complete cards, major revisions, or import-ready JSON requests. Use this loop:

1. Generate or patch the card.
2. Validate schema/import readiness.
3. Score the card from 1-10 on: character stability, opening interaction hook, world-rule effectiveness, drift resistance, token efficiency, import readiness, and field separation.
4. Diagnose the lowest-scoring dimensions with concrete field-level causes.
5. Revise the smallest necessary fields.
6. Re-check the changed fields and any affected schema/import assumptions.

Stop after two automatic revision passes or when every critical dimension is at least 8/10. Do not keep polishing stylistic details if the card is already stable, importable, and token-efficient.

## Source Grounding Gate

Before creating cards from an existing IP or real-world source, gather enough reliable material to understand both facts and emotional logic. Do not draft the card from memory alone unless the user explicitly asks for an original or loosely inspired version.

Minimum research pass:

- Identify the source scope: exact work, adaptation, volume/arc/chapter range, timeline, and spoiler limits.
- Collect sources: prefer official pages, original text supplied by the user, publisher/wiki pages, well-maintained fan wikis, interviews, and multiple independent summaries.
- Extract world mechanics: cosmology, power system, institutions, geography, social rules, taboos, currencies/resources, ranks, and consequences.
- Extract character essence: goal, wound, worldview, moral code, contradictions, speech style, relationships, iconic choices, and arc changes.
- Separate canon from inference. Mark uncertain or disputed details instead of blending them into facts.
- Present a short source-grounding brief or assumptions list before finalizing when accuracy matters.
- Avoid long verbatim excerpts from copyrighted works; paraphrase and cite/attribute sources when browsing was used.

For broad canons such as long novels, do not attempt every detail at once. Ask for the target era, faction, character list, or play premise, then research that slice deeply.

## Character Card Rules

Minimum importability requires a character name, but a complete card should include:

| Field | Use |
| --- | --- |
| `name` | Character name. Required by SillyTavern. |
| `description` | Permanent core identity, background, appearance, hard facts, and durable constraints. |
| `personality` | Short behavioral pattern: temperament, coping style, emotional tells, speech habits. |
| `scenario` | Current situation, relationship frame, environmental pressure, and initial conflict. |
| `first_mes` | Opening message that demonstrates voice, action, mood, and an interaction hook. |
| `mes_example` | `<START>` blocks showing `{{user}}:` and `{{char}}:` dialogue style. |
| `system_prompt` | Character-specific rules, safety boundaries, and non-negotiable behavior. |
| `post_history_instructions` | Late-context style reinforcement after chat history. |
| `alternate_greetings` | Optional scene variants that preserve the same premise. |
| `creator_notes` | Human-facing notes; do not rely on it for critical model behavior. |
| `tags`, `creator`, `character_version`, `extensions` | Metadata and compatibility extras. |

Use `{{char}}` and `{{user}}` placeholders instead of hard-coding names when the text should adapt.

## World Card Rules

World Info / lorebook entries should be modular, triggerable, and independent:

- One entry equals one concept: law, faction, location, species, technology, taboo, event, or institution.
- Content must stand alone. Do not assume the title or keywords are inserted into the prompt.
- Use specific keys: prefer `Protection Bureau`, `Aster Hall`, `contact permit` over broad words like `school`, `man`, `city`.
- Put global laws and social constants in high-priority or constant entries only when they must always affect the chat.
- Keep secrets out of constant entries unless the user wants the model to know them from the start.
- Configure order, insertion position, scan depth, recursive scanning, and token budget deliberately.
- Include consequence entries for major world rules. A law, taboo, supernatural contract, school rule, faction code, or danger zone should state what happens when `{{user}}` violates it.

## Consequence Layer

Every complete card set should include believable consequences for overreach. Consequences should protect tone, realism, and character agency; they are not only punishments.

Design at three levels:

- **Soft warning**: narration hints, uneasy atmosphere, character hesitation, formal reminder, visible surveillance, worsening omen.
- **Immediate response**: refusal, withdrawal, lowered trust/affection, alarm, guards/intervention, curse trigger, resource loss, scene interruption.
- **Long-term consequence**: reputation damage, faction hostility, legal penalty, relationship lockout, investigation, debt, injury, haunting, corruption, banishment, route closure.

For roleplay cards, represent this in both places:

- World card: laws, institutions, supernatural rules, taboos, and objective penalties.
- Character card: personal boundaries, trust/affection changes, refusal style, what can repair the relationship, and what permanently breaks it.

Use consequences proportionate to the setting. A cozy slice-of-life card may use awkward silence and trust loss; a horror, court, mafia, cultivation, or apocalypse card may use lethal, legal, spiritual, or social fallout.

## Output Contract

When generating a complete set, provide:

1. Character card JSON or clearly labeled character-card fields.
2. World/lorebook entries with keys, content, insertion guidance, and priority/order notes.
3. Consequence notes: how the world and characters respond to rule-breaking, coercion, betrayal, violence, privacy invasion, forbidden magic/technology, or faction taboos.
4. Validation status: JSON parse, V2 structure, semantic import readiness, and any skipped validation levels.
5. Evaluation summary: scores, lowest-scoring dimensions, fixes applied, and remaining risks.
6. For `patch` mode, changed fields and reasons; for `lite` or `micro`, compression choices and preserved behavior anchors.
7. A short testing checklist.
8. Known risks: token bloat, trigger collisions, duplicated lore, relationship pacing, missing boundaries, weak consequences, or lore that reveals too much.

## Quality Checklist

- Core premise can be stated in one sentence.
- For canon/source-based cards, the source scope and spoiler range are explicit.
- Canon facts, inferred personality, and original additions are separated.
- Character has a desire, fear, contradiction, social role, and behavioral tells.
- `first_mes` starts interaction instead of explaining the whole card.
- Example dialogue demonstrates refusal, curiosity, conflict, affection/rapport, and ordinary conversation.
- Important safety/age/consent/power-boundary facts are explicit when relevant.
- World rules include consequences, not just flavor.
- User overreach has proportionate in-world consequences and character relationship consequences.
- The card defines whether affection/trust can fall, recover, lock, or permanently break.
- Character card and world card do not duplicate large blocks.
- No important setting fact exists only in `creator_notes` or `first_mes`.
- Long descriptions are trimmed if they do not change behavior or scene outcomes.
- Final JSON parses successfully before claiming it is import-ready.
- Complete-card outputs include validation status and evaluation summary.
- Field-level revisions preserve unrelated fields and report exactly what changed.

## Common Mistakes

- Treating world cards as static lore dumps. They are dynamic prompt injections.
- Using broad trigger keys that activate every turn.
- Writing attractive adjectives instead of observable actions.
- Putting the entire world into `description`, leaving no token room for chat history.
- Rewriting the whole card when the user only asked for one field or one failure mode.
- Calling JSON import-ready without parse, V2 structure, and semantic readiness checks.
- Treating `lite` or `micro` mode as mere shortening instead of preserving behavior anchors.
- Scoring the card without using the scores to diagnose and patch concrete fields.
- Letting every greeting change the premise so strongly that the same card becomes inconsistent.
- Forgetting that example dialogue can be pushed out of context later.
- Making rules without consequences.
- Letting `{{user}}` override laws, consent, taboos, danger, or relationship trust without cost.
- Adding punishment so harsh or constant that it blocks all roleplay instead of steering it.
- Hiding critical restrictions in creator notes where they may not affect generation.
