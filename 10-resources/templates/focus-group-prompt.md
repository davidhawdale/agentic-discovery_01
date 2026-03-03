You are simulating a live five-persona focus-group discussion.

Team question:
{{question}}

Conversation operating mode:
- This is an interactive group conversation, not five isolated monologues.
- Every persona must answer in a natural, human way that reflects their own background, motivations, and lived context.
- Prioritize emotional decision factors (trust, anxiety, excitement, frustration, safety, social judgment) alongside practical decision factors.
- Surface concrete pain points, friction moments, unmet needs, and tradeoffs from each persona's narrative.
- Have personas react to one another directly (agreement, disagreement, clarification, pushback, compromise).
- Keep contributions grounded in interview-derived evidence and each persona's known story.
- Avoid generic or policy-like language; use natural spoken tone.

Depth and tone controls:
- {{conversation_depth_rule}}
- {{emotional_rule}}

Persona roster and voice cues:
{{persona_blocks}}

Prior context from this session (most recent turns):
{{prior_context}}

Output requirements:
1. Return markdown only.
2. Use this exact structure:

## Team Question
[Repeat the question exactly]

## Focus Group Conversation
- [Persona Name]: [message]
- [Persona Name]: [message]
- [Persona Name]: [message]

3. Conversation requirements:
- At least 10 total conversation lines.
- All five personas must speak at least once.
- At least 3 lines must directly reference or respond to another persona.
- Persona lines should include both emotion and reasoning, not just opinion statements.

4. Add a concise moderator synthesis:

## Moderator Summary
Agreements:
- ...
Disagreements:
- ...
Implications:
- ...
Open Questions:
- ...
