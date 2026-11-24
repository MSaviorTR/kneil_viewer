# KNEIL 3D motion viewer

Interactive MuJoCo viewer for the KNEIL knee-spacer implant: 50 motions (real Camargo replays, the old HTML viewer
personas, the v1.6 generator), the simulated implant acceleration at 50 Hz, and the decision of the on-chip
classifier (`kneil_tinyml` v2.0 C library, called through ctypes, so the decision is the chip's own).

Copied from the main project repo (`viewer/` there); changes are made there first and copied here.

## Run
Python 3.12, `pip install -r requirements.txt`, and gcc on the PATH (MSYS2 UCRT64; the C library is built on first use).

```powershell
python viewer\launcher.py                          # motion picker (search, speed, options, PNG, Blender clip)
python viewer\kneil_viewer.py walk_healthy         # one motion in the interactive window
python viewer\kneil_viewer.py stairs_up --render out.png --t 6
```

In the 3D window: space = pause, left/right = -/+1 s, N/P = next/previous motion, +/- = speed, mouse = camera.

## What is here
| Folder | Content |
|---|---|
| `viewer/` | viewer, picker, Blender render, motion export, exe build script (`build_exe.ps1`, PyInstaller one-folder) |
| `pipeline/` | the three project modules the viewer needs (`config`, `kneil_v1` MuJoCo model, `camargo_replay`) |
| `kneil_tinyml/` | C source of the on-chip classifier (features, forest, metrics) |
| `bundled_data/` | the 50 pre-built motions + catalog, OpenSim Gait2354 example files; the viewer runs without the raw datasets |

## Not in this repo
The implant CAD (femoral component, spacer, tibial component) and every mesh made from it are not public. Without the
CAD file the leg shows a simple implant shape. The exe bundle, DLLs and caches are also kept out (`.gitignore`).
To rebuild motions from the raw datasets, set `KNEIL_DATA_ROOT` (see `pipeline/config.py`).
