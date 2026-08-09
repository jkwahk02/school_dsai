# DS & AI Courses — Common Lab Setup (do this ONCE)

This one-time setup works for **all** of our data-science courses. Do it **once** at the start
of the semester; after that, each course only needs its own short setup note (which reuses this).

Once set up, the course notebooks run **fully offline on your laptop** — no Google, Colab,
Kaggle, or VPN needed. Internet is required **only during installation**.

---

## 0. What each course gives you
A course folder containing: the notebook(s) (`.ipynb`), a **`data/`** folder, an
**`environment.yml`**, and a short **`<COURSE>_SETUP.md`** note. Keep each course in its own folder.

---

## 1. Install Miniconda — once, for all courses
1. Download the Windows/Mac installer: https://docs.conda.io/en/latest/miniconda.html
   - If the download is slow, use the Tsinghua mirror:
     https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/
2. Run the installer (default options are fine).

> **Tip (recommended): install Miniforge instead of Miniconda.**
> https://github.com/conda-forge/miniforge — it defaults to the free `conda-forge` channel
> (no Anaconda "Terms of Service" prompts) and ships the **fast `mamba` solver**, which avoids the
> slow "Solving environment" hang described below. If you use Miniforge, replace `conda` with
> `mamba` in the commands here.

---

## 2. (China) Set download mirrors — once
Open **"Anaconda Prompt"** (Windows) or a terminal (Mac) and paste:

```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --set show_channel_urls yes
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

> Without the mirrors, `conda env create` can be very slow or stall in China.

---

## 3. Per-course workflow
Each course arrives as a folder containing its own `environment.yml`. Using it has two parts:
a **one-time** build, then a **quick launch** each time you study.

### First time for a course — build its environment (once)
1. Open **Anaconda Prompt** (Windows) or a **Terminal** (Mac).
2. Go into the course folder — type `cd ` (with a space) and drag the folder onto the window, or type the path:
   ```bash
   cd path/to/DA321
   ```
3. Create the environment. This installs everything the course needs and **takes a few minutes**:
   ```bash
   conda env create -f environment.yml
   ```
   You only do this **once per course**.
   > **If it hangs on `Solving environment` for many minutes**, use the fast solver:
   > ```bash
   > conda env create -f environment.yml --solver=libmamba
   > ```
   > (Miniforge users: `mamba env create -f environment.yml` — fastest.)

### Every time you want to work — activate and launch
4. Activate the course's environment. Its name is given in the course note (e.g. `da321`):
   ```bash
   conda activate da321
   ```
   ⚠️ **Check the prompt now shows `(da321)`, not `(base)`.** This is the #1 mistake — if you run
   `pip`/`conda`/`jupyter` while still in `(base)`, you're using the wrong environment and things
   won't work. Always confirm `(da321)` before continuing.
5. Start JupyterLab:
   ```bash
   jupyter lab
   ```
   Your browser opens automatically. Open the course notebook (the `.ipynb` file) and run the
   cells — menu **Run ▸ Run All Cells**.

**When you're done:** close the browser tab and press `Ctrl + C` in the terminal to stop JupyterLab.

**Good to know**
- Each course has its **own** environment name, so they never conflict — switch between courses with
  `conda activate <name>`.
- The build in step 3 is the only step that needs internet. **After that, everything runs offline.**

---

## General troubleshooting (applies to any course)
- **`Solving environment` spins for a long time** → not an error, just the slow default solver.
  Cancel with `Ctrl + C` and retry with the fast solver:
  `conda env create -f environment.yml --solver=libmamba` (or use Miniforge's `mamba`).
- **Commands "don't work" / package not found** → you're probably in `(base)`. Run
  `conda activate <env>` and confirm the prompt shows `(<env>)` before retrying.
- `conda env create` still stalls → confirm the mirrors in step 2, then retry.
- Wrong/old packages → rebuild the env:
  `conda env remove -n <env>` then `conda env create -f environment.yml`.
- "File not found" for data → keep the `data/` folder **next to the notebook**; notebooks load
  local paths like `data/xxx.csv` (no upload needed).
- Plotly figure is blank → in JupyterLab it renders offline by default; restart the kernel and
  rerun. Do **not** use the `notebook_connected` renderer — it needs internet.

---

➡️ **Next:** open your course's own note (e.g. `DA321_SETUP.md`) for its environment name and any
course-specific steps.
