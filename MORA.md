# Mora 0.3 — working language contract

Mora is **affective, evidence-driven and goal-directed**.

A Mora program does not primarily say “call this function when that callback fires”. It describes:

- what the program **remembers**;
- what it **believes**, including uncertainty;
- how observations acquire **meaning**;
- patterns inferred from histories of evidence;
- what the program **desires**;
- emotional/behavioural **journeys** it tries to follow;
- **offers** it can expose or withdraw;
- **laws** that must remain true;
- external **faculties** supplied by the runtime;
- declarative **scenes** through which humans interact with it.

## Core forms

### belief

```mora
belief user about emotion {
    confident  0.4
    uncertain  0.3
    never certain
}
```

Beliefs are distributions/evidence accumulators, not booleans.

### meaning

```mora
meaning repeated correction(frame) within 12s {
    suggests frustrated strongly
}
```

Meaning transforms observations into evidence.

### pattern

```mora
pattern user struggles with frame {
    repeated correction(frame)
    or undo soon after correction(frame)
}
```

Patterns operate over histories, beliefs and relations.

### desire

```mora
desire DetectPhotos {
    requires scan
    ask vision to perceive PhysicalPhoto in scan.image

    fulfilled with candidates {
        remember frames
        perceive detection succeeded
    }
}
```

A desire describes an intended outcome. The runtime chooses the execution machinery.

### journey

```mora
journey Editing {
    toward user.confident
    away from user.frustrated
}
```

A journey is a continuously evaluated behavioural objective.

### law / preference

Laws are invariants. Preferences rank acceptable outcomes without turning every decision into hand-written branching.

### faculty

A faculty is a typed capability supplied by the runtime or an external library. Application code can depend on a faculty without containing that library's host-language implementation.

### scene

A scene declares an interactive surface. Gestures produce perceptions or desires; the runtime owns callbacks and toolkit glue.

## Deliberately absent from application-level Mora

Normal Mora application code should not need:

```
fn
class
lambda
callback
state.foo =
widget.connect(...)
```

Those belong below the language boundary.
