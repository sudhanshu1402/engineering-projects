# Cartoonify Image

A small Python script that turns a photo into a cartoon-style image using classic OpenCV image filters. There's no machine learning model here despite the folder name — it's a hand-built image-processing pipeline with a tiny Tkinter GUI.

## What it does

The cartoon look comes from combining two things: bold black outlines and flat, smoothed color regions. The script builds both separately, then overlays them:

1. Read the image and convert it from OpenCV's BGR to RGB.
2. Make a grayscale copy.
3. Median-blur the grayscale to remove speckle.
4. Run adaptive thresholding on the blurred grayscale to pull out edges as a black-and-white mask.
5. Bilateral-filter the original color image — this smooths flat areas while keeping edges crisp.
6. Combine the smoothed color image with the edge mask (`bitwise_and`) to get the cartoon.

It then plots all six stages side by side in a matplotlib grid so you can see the transformation, and gives you a button to save the result.

## Stack

- **Python 3**
- **OpenCV (`cv2`)** — all the actual image processing
- **matplotlib** — the 6-panel before/after plot
- **Tkinter** — the small window with the two buttons
- **Pillow, numpy** — pulled in as dependencies of the above

Note: the script also imports `easygui` and `imageio`, but they aren't actually used — leftovers from the tutorial this was built from.

## Run it

Install the libraries:

```bash
pip install opencv-python matplotlib pillow numpy
```

Run:

```bash
python cartoonify_image.py
```

A 400x400 window opens with a **Cartoonify an Image** button. Click it to process the image and see the six-stage plot; a **Save cartoon image** button then writes the result next to the source file as `cartoonified_Image.jpg`.

## Heads up: the input path is hardcoded

The `upload()` function does **not** open a file picker. It points at a fixed Windows path:

```python
ImagePath = "C:/Users/admin/PycharmProjects/Cartoonify Image with Machine Learning/bros.jpg"
```

To run this on your own machine, edit that line to point at a real image — for example the bundled `bros.jpg`:

```python
ImagePath = "bros.jpg"
```

A sample image (`bros.jpg`) is included in this folder to test with.

## Input

![bros](https://user-images.githubusercontent.com/99204211/183352481-3b72fe53-556a-4e49-aef8-62599933ba53.jpg)

## Output

![image](https://user-images.githubusercontent.com/99204211/183352754-79aab67b-5873-4ec9-a407-e5ad5a66f6c8.png)

## Scope

This is a learning exercise, not a polished tool. The input path is fixed in code, unused imports are left in, and there's no error handling beyond a check for a missing file. It's a good, readable example of building a cartoon effect from OpenCV primitives.
