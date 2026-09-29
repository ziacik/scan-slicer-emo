# Scan Slicer Emo

A full GTK4/libadwaita application written in **Mora 0.4**.

The application contains the domain logic. Mora itself does not know what a photo, region, scan, detection desire, export desire, or Scan Slicer is.

## What lives here

- the `PhysicalPhoto` concept and OpenAI prompt
- detection thresholds and dedupe settings
- scanner/open/export workflows
- application state such as `scan`, `regions`, `selection`, and `padding`
- UI scene, buttons, gestures, and adaptive editing behavior
- the emotional evidence model

For example:

```mora
concept PhysicalPhoto {
    describe "Detect only separate physical photographic prints ..."
    result list of Quad
}
```

and:

```mora
desire DetectRegions {
    requires scan.image
    attempt vision.perceive scan.image PhysicalPhoto as candidates
    attempt geometry.filter candidates scan.image 0.04 0.003 0.80 3 0.02 as candidates
    attempt geometry.dedupe candidates 0.85 as candidates
    remember regions as candidates
}
```

Mora only provides generic execution verbs and faculties.

## Install

On Arch/Manjaro:

```bash
sudo pacman -S python python-gobject gtk4 libadwaita python-pillow python-opencv python-requests sane libsecret

git clone https://github.com/ziacik/mora.git
cd mora
sh install.sh

cd ..
git clone https://github.com/ziacik/scan-slicer-emo.git
cd scan-slicer-emo
mora check app.mora
mora run app.mora
```

## Source layout

```
app.mora
src/
  emotion.mora
  geometry.mora
  io.mora
  vision.mora
  editor.mora
  ui.mora
```
