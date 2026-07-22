# Color Detection

Double-click anywhere in an image and it tells you the color name and RGB values under your cursor.

## What it does

You pass in an image, an OpenCV window opens, and every time you double-click a pixel the program reads its BGR value, finds the closest named color from a lookup table of 865 colors, and draws a filled bar across the top of the window showing the name and R/G/B numbers.

"Closest" is a plain Manhattan distance in RGB space: `|R-r| + |G-g| + |B-b|` summed against every row in `colors.csv`, keeping the smallest. No fancy color science, just the nearest match by absolute difference. For very light pixels (`R+G+B >= 600`) the text is redrawn in black so it stays readable on the light bar.

It's a small learning project built on the standard OpenCV color-detection tutorial.

## Stack

- Python
- [OpenCV](https://pypi.org/project/opencv-python/) (`cv2`) — image reading, window, mouse callback, drawing
- [pandas](https://pypi.org/project/pandas/) — reads the color table
- `argparse` — image path from the command line

No `requirements.txt` in the repo; install the two libraries directly:

```bash
pip install opencv-python pandas
```

## Files

| File | What it is |
|------|------------|
| `color_detection.py` | The whole program |
| `colors.csv` | 865 named colors: slug, display name, hex, R, G, B (no header row) |
| `colorpic.jpg`, `colorpic2.jpg` | Sample images to try it on |

## Run

```bash
python color_detection.py -i colorpic.jpg
```

The `-i` / `--image` argument is required. Then:

- **Double-click** any pixel to detect its color.
- **Esc** to quit.

Run it from inside this directory — the script opens `colors.csv` by a relative path, so it has to find it in the current working directory.

## Example

Double-click a blue patch and the top bar fills with that blue and shows something like:

```
Cornflower Blue R=100 G=149 B=237
```

## Notes

- The mouse callback stores BGR from OpenCV (`b, g, r = img[y, x]`) and correctly reorders to RGB before matching — worth noting since OpenCV loads images as BGR, not RGB.
- The nearest-color loop iterates all 865 rows on every click. Fine for one image; it's O(n) per click, not indexed.
- The `.replit` file points at `Color_Detection.py` (capitalized), but the actual file is `color_detection.py`. Use the lowercase name when running locally.
- Needs a display — it opens a GUI window, so it won't work over a plain headless session.
