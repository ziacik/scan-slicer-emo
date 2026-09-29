# Scan Slicer Emo

A real application written in **Mora 0.3**, an affective programming language.

The important bit is not the file extension. The application is expressed in Mora's own primitives: **beliefs, meanings, patterns, desires, journeys, offers, perceptions and laws**. There are no user-defined `fn` functions, callback wiring, mutable `state.foo` assignments, or hand-written GTK control flow in the app.

Native libraries are exposed to Mora as **faculties**. GTK/libadwaita can render a scene, OpenCV can perform a perspective crop, SANE can acquire a scan, and OpenAI can act as a vision faculty. The application decides *what it wants and how evidence should change its behaviour*.

## Example

```mora
journey Editing {
    toward user.confident
    away from user.frustrated

    when user struggles with current frame {
        offer PreciseEditing
    }

    when user flows {
        withdraw PreciseEditing
    }
}
```

The emotion model is uncertain by design:

```mora
belief user about emotion {
    confident   0.45
    uncertain   0.20
    frustrated  0.05

    never certain
    fades toward neutral over 45s
}
```

Interaction evidence changes that belief:

```mora
meaning repeated correction(frame) within 12s {
    suggests frustrated strongly
    suggests uncertain moderately
}
```

The UI itself is declarative:

```mora
gesture drag focused frame.edge {
    move edge preserving vector
    respecting EditableFrame
}
```

## Application features

- GTK4/libadwaita desktop UI
- PNG/JPEG/TIFF opening
- SANE scanning
- OpenAI physical-photo detection
- system-keyring API key
- skewed/rotated quadrilateral frames
- corner, edge and whole-frame editing
- pan/zoom
- undo/redo
- perspective-correct full-resolution export
- adaptive magnifier, handles and snapping driven by the affective journey

## Source layout

```
app.mora
src/
  emotion.mora
  geometry.mora
  scanner.mora
  vision.mora
  editor.mora
  ui.mora
```

## Run

Requires a Mora 0.3 runtime with the faculties declared by this application.

```bash
mora check app.mora
mora run app.mora
```

The app repository intentionally contains no implementation of those native faculties. They belong to the Mora runtime, in the same way a language runtime provides I/O and platform bindings without making the application itself Python/Rust/C.
