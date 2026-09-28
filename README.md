# Scan Slicer Emo

A full GTK4/libadwaita Scan Slicer experiment written in **Mora**, an affective programming language.

There is no Rust, Python, C, or JavaScript application code in this repository. The app source is `.mora`; native functionality is reached through Mora's FFI/runtime bindings.

## What works

- GTK4/libadwaita desktop UI
- open PNG/JPEG/TIFF scans
- scan via SANE `scanimage`
- OpenAI vision detection of physical photo prints
- API key stored through the system keyring (`secret-tool`/libsecret)
- editable quadrilateral frames, including rotated/skewed prints
- corner and whole-edge dragging
- pan and zoom
- undo/redo
- full-resolution perspective-corrected PNG export
- adaptive magnifier, larger handles and stronger edge snapping when the interaction model becomes uncertain/frustrated

The emotional model is deliberately a **belief state inferred from interaction evidence**. The app never claims that it knows the user's actual emotion.

## Dependencies on Arch/Manjaro

```bash
sudo pacman -S python-gobject gtk4 libadwaita python-pillow python-opencv python-requests sane libsecret
```

You also need the Mora runtime (`mora` command).

## Run

```bash
mora check app.mora
mora run app.mora
```

## The affective part

The application declares an emotional belief state directly in Mora:

```mora
emotion user:
    confident = 0.45
    uncertain = 0.20
    frustrated = 0.05
```

Real UI events become evidence:

```mora
observe user, "corner_drag", amount=1.0
```

The app then adapts with normal Mora control flow:

```mora
when user.frustrated >= 0.68 or user.uncertain >= 0.78:
    state.assist = "strong"
```

Strong assistance enables larger drag handles, a stronger snap radius, and a live magnifier while editing.
