# DA321 — Course Setup Note

> **First time?** Do the one-time steps in **`SETUP_common.md`** first (install Miniconda +
> set the China mirrors). You only ever do that once, for all courses.
> This note covers only what is specific to **DA321**.

---

## Set up and run
In the DA321 course folder (it contains `environment.yml`, the notebook, and the `data/` folder):

```bash
conda env create -f environment.yml
conda activate da321
jupyter lab
```

Then open **`DA321_Fall_2026_Local.ipynb`** and run the cells (Run All).
All data loads from the local `data/` folder — **fully offline**, no uploads or downloads.

---

## What DA321 installs
A heavier stack than most courses (all handled automatically by `environment.yml`):
- **Geospatial:** geopandas, rasterio, shapely, folium
- **Graphs:** graphviz, pygraphviz, pydot, networkx
- **Also:** plotly, wordcloud, statsmodels, scikit-learn, factor-analyzer, pyarrow, …

The first `conda env create` takes a few minutes because of these packages.

---

## Optimization cell (OR-Tools / CP-SAT) — may need one extra step on Windows
One cell demonstrates **Constraint Optimization with Google OR-Tools (CP-SAT)**. On some Windows
machines its native library fails to load with **`OSError: [WinError 127]`** and a popup
**"python.exe — 시작 지점 없음 …"**. The notebook handles this gracefully:

- **Just click 확인 (OK)** on the popup. The notebook prints `[optional] ortools ... skipped` and
  **continues** — only that one CP-SAT cell is skipped; everything else runs normally.

The current `environment.yml` already keeps `pyarrow` on **pip** specifically to avoid this clash,
so a **fresh `conda env create` should import OR-Tools fine**. If you still hit `WinError 127`
(some package pulled conda's Abseil back in), repair the env once, then restart the kernel and re-run:
```bash
conda activate da321
conda remove --force pyarrow libprotobuf libabseil -y
pip install --force-reinstall pyarrow
```
(Root cause: conda-forge's `pyarrow` drags in a `libabseil`/`libprotobuf` that shadows the Abseil
OR-Tools bundles. Using the self-contained pip `pyarrow` removes the conflict.) If it still fails,
ensure the **Microsoft Visual C++ 2015–2022 Redistributable (x64)** is installed:
https://aka.ms/vs/17/release/vc_redist.x64.exe

---

## DA321-specific troubleshooting
- **pygraphviz** fails → `conda install -c conda-forge graphviz pygraphviz`
- **NYC-taxi cell** errors reading `.parquet` → `pyarrow` is required (already in `environment.yml`;
  rebuild the env if you changed it).
- **Excel-export cell** errors (`No module named 'openpyxl'`) → `openpyxl` is required (already in
  `environment.yml`; rebuild if you changed it).
- **Hong Kong DEM cell** is compute-heavy (SRTM elevation tiles) — it may take a little while to
  render. That is normal.
- **Plotly** figure blank → `import plotly.io as pio; pio.renderers.default = "notebook"`
  (offline; do not use `notebook_connected`).

> Note: `environment.yml` intentionally pins **numpy<2, pandas<2.2, scikit-learn<1.6** so that the
> course's older packages (joypy, factor_analyzer, OR-Tools, …) stay compatible. Don't upgrade these.

---

## Data
Every dataset ships inside `data/` (~67 MB total), including the elevation tiles in `data/dem/`.
Nothing to download. See **`data/README.md`** for a description of each file.
