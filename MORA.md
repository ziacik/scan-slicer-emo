# Mora 0.4 contract used by this application

Mora is affective, evidence-driven, and goal-directed.

Application code is built from:

- `belief` — uncertain state inferred from evidence
- `meaning` — how perceptions change beliefs
- `pattern` — temporal/evidential patterns
- `journey` — continuously evaluated goals
- `desire` — an intended workflow
- `faculty` — a generic capability supplied by the runtime
- `concept` — application-owned semantic description
- `scene` — declarative interactive UI
- `law` and `preference` — constraints and priorities

Mora 0.4 desires are executed generically. There is no runtime dispatch such as “if desire is DetectRegions”. A desire is interpreted from verbs like:

```mora
ask files.choose-image as source
attempt images.load source as image
remember document as image
snapshot items selection into history
for every item in items { ... }
perceive changed(item)
```

Application-specific concepts, prompts, names, thresholds, and workflows belong in the application repository.
