---
name: learn-from-your-ask
description: Capture valuable technical learning from the current AI conversation into a persistent personal knowledge graph. Use when the user asks to save, learn from, record, or visualize recent technical Q&A, especially via /learn-from-your-ask.
---

# learn-from-your-ask

Capture the most recent valuable technical Q&A from the current conversation and add it to a local learning knowledge graph.

## Output Locations

Use paths relative to the current workspace unless the user gives another target:

- Knowledge data: `knowledge/knowledge.json`
- Generated visualization: `knowledge/index.html`
- HTML template: `templates/graph.html`

Create `knowledge/` and `knowledge/knowledge.json` if they do not exist.

## Filtering Rules

Skip saving when any rule applies:

- The conversation is casual chat, greetings, status updates, or off-topic.
- There is no technical concept, code, tool, framework, architecture, debugging, or workflow knowledge.
- The user question is too short and contains no technical terms.
- The topic is only about operating Claude Code, agent settings, slash commands, or this skill itself.
- The assistant answer is a refusal or does not contain useful explanation.
- The point is a near-duplicate of an existing record in `knowledge/knowledge.json`.

Save when the exchange teaches or clarifies a reusable technical concept, workflow, implementation detail, debugging pattern, or design decision.

## Knowledge Schema

Maintain this shape:

```json
{
  "version": "1.0",
  "profession": "",
  "domains": {
    "Backend": {
      "FastAPI": [
        {
          "topic": "Dependency injection",
          "tags": ["python", "fastapi", "dependency-injection"],
          "date": "2026-06-29",
          "question": "Concise summary of the user's question.",
          "answer": "Concise summary of the assistant's answer.",
          "conversation": [
            {"role": "user", "content": "..."},
            {"role": "assistant", "content": "..."}
          ]
        }
      ]
    }
  }
}
```

Use English domain names by default unless the existing knowledge base already uses another language.

Common domains:

- `Backend`: APIs, server frameworks, databases, queues, auth, services
- `Frontend`: React, Vue, CSS, browser APIs, UI behavior
- `Database`: SQL, indexes, schema design, ORM behavior
- `DevOps`: Docker, Kubernetes, CI/CD, deployment, cloud
- `Algorithms`: data structures, algorithms, LeetCode, complexity
- `System Design`: architecture, design patterns, scaling, tradeoffs
- `Programming Language`: syntax, runtime behavior, async, decorators, type systems
- `AI Engineering`: prompts, agents, RAG, tool use, model integration

## Workflow

1. Read `knowledge/knowledge.json` if it exists. If it does not exist, initialize the schema above with empty `profession` and `domains`.
2. Inspect the latest 1-3 meaningful user/assistant exchanges in the current conversation.
3. Apply the filtering rules. If nothing should be saved, tell the user no valuable technical knowledge point was detected.
4. Check for near-duplicates in the existing knowledge base by comparing domain, subdomain, topic, question, and tags.
5. Add one knowledge point under `domains[domain][subdomain]`.
6. Read `templates/graph.html`, replace `{{KNOWLEDGE_DATA}}` with the complete JSON object, and write `knowledge/index.html`.
7. Tell the user what was saved, where it was categorized, and the path to `knowledge/index.html`.

## Implementation Notes

- Preserve existing knowledge records.
- Keep `knowledge/knowledge.json` valid JSON with two-space indentation.
- Do not overwrite `templates/graph.html`.
- If `templates/graph.html` is missing, still update `knowledge/knowledge.json` and report that visualization generation was skipped.
- Prefer concise summaries over copying full long responses, but keep enough conversation context to reconstruct the learning point.
