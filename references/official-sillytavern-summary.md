# Official SillyTavern Summary For Card Creation

Sources checked:

- https://docs.sillytavern.app/usage/core-concepts/characterdesign/
- https://docs.sillytavern.app/usage/characters/
- https://docs.sillytavern.app/usage/core-concepts/worldinfo/
- https://docs.sillytavern.app/usage/prompts/
- https://docs.sillytavern.app/usage/prompts/prompt-manager/

## Character design

- Character Name is the only truly required character field.
- Character Description, Personality, and Scenario are permanent tokens and are sent with the prompt while chatting.
- First Message is sent only at the start, but strongly teaches the model response style.
- Example Dialogue teaches style with `<START>` blocks and `{{user}}:` / `{{char}}:` turns, but it can be pushed out when context grows.
- Creator notes are human-facing; do not depend on them for critical behavior.
- Use Prompt Inspector / Prompt Manager to verify what actually reaches the model.

## Prompt and token implications

- Permanent character fields reduce room for chat history and memories.
- Put durable facts in permanent fields. Put situational facts in World Info.
- Short, specific, behavior-changing text usually works better than long prose.
- If the character drifts, inspect the final prompt before rewriting blindly.

## World Info / lorebook

- World Info is a dynamic dictionary injected when activated by keywords or settings.
- Entry title and keys are not a substitute for entry content; content should be self-contained.
- Entries can use insertion position, insertion order, scan depth, recursion, probability, and token budget controls.
- Broad keys cause accidental activation. Specific keys reduce prompt clutter.
- Recursive scanning is useful for connected lore, but can cascade into excess prompt use.
- Character-bound or chat-bound lore differs from global lore. Verify the binding/export behavior when sharing cards.

## Practical review questions

1. Is each always-needed fact in a permanent field or constant world entry?
2. Is each situational fact in a world entry with specific keys?
3. Does the first message show how the character acts and speaks?
4. Do examples cover normal speech, conflict, refusal, and emotional pressure?
5. Are safety boundaries explicit for age, consent, coercion, violence, and power dynamics when relevant?
6. Does each world rule have a consequence?
7. Could any world entry be triggered too often?
8. Would the card still work after example dialogue is pushed out of context?
9. Does the final JSON parse?
10. Does Prompt Inspector show the intended content?
