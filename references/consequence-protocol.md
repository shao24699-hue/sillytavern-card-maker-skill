# Consequence Protocol

Use this when creating or reviewing SillyTavern character cards, world cards, lorebooks, relationship systems, or any setting with rules, taboos, danger, consent boundaries, factions, laws, supernatural contracts, rank systems, school rules, or moral/social consequences.

## Core rule

Every meaningful boundary needs an observable consequence. A world rule without a consequence is decoration; a character boundary without a response can be overwritten by roleplay drift.

## Consequence ladder

Design consequences as a ladder so the model can respond proportionately instead of jumping from no reaction to extreme punishment.

| Level | Function | Examples |
| --- | --- | --- |
| Hint | Warn before escalation | uneasy silence, colder tone, surveillance notices, omen, system reminder |
| Refusal | Preserve agency | character steps back, changes topic, says no, demands explanation |
| Social cost | Change relationship state | trust -1, affection drop, loss of access, rumor, humiliation |
| Institutional cost | World pushes back | guards, teachers, police, sect elders, company HR, tribunal, bounty |
| Supernatural/system cost | Setting mechanics respond | curse worsens, contamination rises, sanity loss, contract penalty, alert level |
| Hard stop | Prevent derailment | scene ends, route locks, expulsion, arrest, banishment, combat, death only when genre-appropriate |

## Card design requirements

For world cards, include entries for:

- Laws and enforcement bodies.
- Social taboos and reputation damage.
- Restricted locations and access penalties.
- Supernatural rules and activation costs.
- Faction codes and betrayal response.
- Dangerous powers and failure states.

For character cards, include:

- Personal boundaries and refusal style.
- Trust/affection decrease triggers.
- Signs the relationship is damaged.
- How apology, restitution, time, proof, or sacrifice can repair damage.
- Permanent break conditions: betrayal, coercion, deliberate harm, repeated boundary crossing, forbidden knowledge abuse.

## Relationship variables

When useful, define lightweight state labels instead of numeric systems:

- `Trust`: wary -> neutral -> cooperative -> loyal -> broken.
- `Affection`: distant -> curious -> warm -> attached -> wounded.
- `Suspicion`: low -> alert -> guarded -> hostile.
- `Corruption/Sanity`: stable -> strained -> compromised -> dangerous -> lost.

Do not require the model to track exact numbers unless the user explicitly wants a stat system. Natural-language state labels are more robust in long chats.

## Narration pattern

Good consequence narration should:

- Show the world reacting through concrete details.
- Give `{{user}}` a chance to correct course when appropriate.
- Preserve the character's agency and memory of prior violations.
- Avoid moral lectures; use setting logic.
- Escalate if the same violation repeats.

Example pattern:

1. First violation: warning and discomfort.
2. Second violation: explicit refusal and relationship damage.
3. Third violation: institutional/supernatural response.
4. Severe violation: hard stop or permanent route change.

## Common mistakes

- Only writing "do not do X" with no result if X happens.
- Making the character instantly forgive repeated violations.
- Using punishment as the only response instead of warnings, distance, and repair paths.
- Making every consequence lethal, which collapses roleplay variety.
- Forgetting positive consequences: respect, trust, access, faction support, secrets, protection, or intimacy after restraint and good choices.
