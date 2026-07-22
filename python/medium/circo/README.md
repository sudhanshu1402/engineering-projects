# circo

Turns a list of map obstacles (lat/long + radius) into a KML file you can open in Google Earth, drawing each one as a circle.

## What it does

`create.py` reads obstacle records from `input.txt`, generates a 500-point circle around each center point, and writes the circles as red line strings to `circle2.kml`. The input format looks like drone/UAS "stationary obstacle" data — cylinders defined by height, radius, latitude, and longitude.

The radius in the input is treated as feet and converted to meters (`* 0.3048`). Circle points are computed with a flat-earth approximation of degrees-per-meter, which is fine for the small radii here (the code notes it stays reasonably accurate under ~100 km).

## Stack

- Python 3
- [`simplekml`](https://pypi.org/project/simplekml/) for writing the KML

## Setup & run

```bash
pip install simplekml
python create.py
```

The script hardcodes the input file (`input.txt`) and output file (`circle2.kml`), so run it from this directory. It writes `circle2.kml` next to itself.

Note: the included `.replit` config points at `Create.py` (capital C); the actual file is `create.py`. Run `python create.py` directly.

## Input format

`input.txt` holds JSON-ish records. The parser is line-based, not a real JSON parse — it scans for lines containing `latitude`, `longitude`, and `cylinder_radius` and pulls the value after the colon:

```
"stationary_obstacles": [
    {
        "cylinder_height": 750,
        "cylinder_radius": 33,
        "latitude": 21.324898,
        "longitude": 74.957593
    },
    ...
]
```

## How the circle is built

For each obstacle, `GenCirc` walks 500 angles around the full circle and offsets the center by `radius * cos(angle)` / `radius * sin(angle)`, converting meters to degrees:

```python
point[1] = centerLat + (180 / math.pi) * (dy / 6378137)
point[0] = centerLon + (180 / math.pi) * (dx / 6378137) / math.cos(centerLat * math.pi / 180)
```

`6378137` is the earth's radius in meters. The longitude offset is divided by `cos(lat)` to correct for meridians converging away from the equator.

## Scope

Practice script, not a library. A few rough edges worth knowing:

- Values are pulled by string matching, so the input has to keep one field per line in the expected order.
- `extract()` mixes `for i in file` with `file.readlines()` and returns inside the loop — it happens to work for this input but is fragile.
- Filenames, circle color, line width, and point count (500) are all hardcoded.
