# Gender & Age Detection

Predicts a person's gender and rough age bracket from a face in an image (or a live webcam feed) using pre-trained OpenCV DNN models.

## What it does

`gad.py` runs three neural networks in sequence:

1. **Face detection** — a Caffe/TensorFlow SSD locates faces and draws a green box around each one.
2. **Gender classification** — predicts `Male` or `Female`.
3. **Age classification** — predicts one of eight age buckets: `(0-2)`, `(4-6)`, `(8-12)`, `(15-20)`, `(25-32)`, `(38-43)`, `(48-53)`, `(60-100)`.

For each detected face it prints the result to the console and overlays a `Gender, Age` label on the image, shown in an OpenCV window.

This is a practice project built on well-known pre-trained models (the Levi & Hassner age/gender nets plus OpenCV's face detector). It is a wrapper around those models, not a from-scratch training exercise. Age output is a coarse bracket, not an exact number — accuracy depends heavily on lighting, angle, and image quality.

## Stack

- Python 3
- OpenCV (`cv2`) — the `dnn` module does all the inference; no other Python deps.

## Model files (required, not included)

The script loads six weight/config files from the working directory that are **not** committed to this repo. Download them before running:

- `opencv_face_detector.pbtxt`
- `opencv_face_detector_uint8.pb`
- `age_deploy.prototxt`
- `age_net.caffemodel`
- `gender_deploy.prototxt`
- `gender_net.caffemodel`

These are the standard OpenCV face detector and the Levi–Hassner age/gender Caffe models, widely mirrored online. Place all six next to `gad.py`.

## Run

Install OpenCV:

```bash
pip install opencv-python
```

Run on one of the sample images:

```bash
python gad.py --image girl1.jpg
```

Run on your webcam (omit `--image`):

```bash
python gad.py
```

Sample images included in the repo: `girl1.jpg`, `girl2.jpg`, `kid1.jpg`, `man1.jpg`, `woman1.jpg`, `woman3.jpg`, `minion.jpg`. `output.jpg` is a saved example of an annotated result.

## Example

```
$ python gad.py --image man1.jpg
Gender: Male
Age: 25-32 years
```

The annotated frame opens in a window titled "Detecting age and gender". Press any key to close.

## Implementation notes

- `highlightFace()` keeps only detections above a 0.7 confidence threshold.
- Each detected face is cropped with 20px of padding before being fed to the gender/age nets, so labels stay near the head.
- The gender/age blobs use the fixed mean values `(78.43, 87.77, 114.90)` and a 227×227 input, matching how the Levi–Hassner models were trained.
- When no `--image` is given, `cv2.VideoCapture(0)` opens the default camera. If no face is found in a frame it prints `No face detected`.

## Caveats

- Age is a bracket, not a year, and both models reflect the biases of their training data — treat predictions as approximate.
- Missing model files will cause OpenCV to fail on the `readNet` calls; this is the most common startup error.
