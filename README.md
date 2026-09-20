# hotice2027.github.io

Project page for **HOTICE: Whole-Body Humanoid Object Transportation in Cluttered
Environments**, served at https://hotice2027.github.io/.

## Layout

| Path | Contents |
| --- | --- |
| `index.html` | The page — the only page |
| `style.css` | Its styles |
| `figs/` | Every video and figure the page uses |

The page runs top to bottom as Abstract → Method → Simulation Results → Real-World Results.

### What is in `figs/`

| Files | Used by |
| --- | --- |
| `teaser.mp4` | Teaser under the title |
| `method.jpeg` | Method figure |
| `rollout_rand1-8`, `rollout_typi1-4` | Simulation Results, first row |
| `rollout_real1-13` (no 7) | Simulation Results, second row |
| `rollout_sphere_*`, `rollout_cylinder_*` | Simulation Results, third row |
| `real1-8.mp4` | Real-World Results row |
| `real_complete.mp4` | Full pick-up-and-deliver clip |
| `logo.png` | Favicon |

## Video encoding

Browsers other than Safari will not decode HEVC, and several source clips arrive that
way (anything exported as `.mov` generally does). Convert before committing:

```sh
ffmpeg -i input.mov -c:v libx264 -profile:v high -pix_fmt yuv420p \
       -crf 23 -preset medium -r 30 -an -movflags +faststart figs/output.mp4
```

Drop `-an` and add `-c:a aac -b:a 128k` to keep the audio. `+faststart` lets playback
begin before the whole file has downloaded. Check what a file actually contains with:

```sh
ffprobe -v error -select_streams v:0 -show_entries stream=codec_name,width,height \
        -of csv=p=0 figs/some.mp4
```

The `.mov` masters stay out of git (see `.gitignore`); commit the encoded `.mp4` only.

## Still to fill in

- Author names and affiliations — currently "Anonymous Authors" for review
- Venue line under the authors, commented out in `index.html`
- Links to the paper, arXiv and code (the quick-links row was removed; add it back when
  there is something to link to)

## Local preview

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
