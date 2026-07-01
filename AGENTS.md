# AGENTS.md

## Project

This repository contains `COMP9517_Lab3.ipynb` — a Jupyter notebook for COMP9517 Lab 3 that trains and compares **KNN**, **Decision Tree**, and **SGD** classifiers on the **Chinese MNIST** dataset (15,000 grayscale 64×64 images, 15 classes).

## Cursor Cloud specific instructions

### Dependencies
Python deps are installed system-wide by the startup update script (see `requirements.txt`). No virtualenv is used; run everything with the system `python3`. The console scripts (`jupyter`, etc.) are installed to `~/.local/bin`, which is not always on `PATH` — prefer invoking tools as modules, e.g. `python3 -m jupyter ...` and `python3 -m nbconvert ...`.

### Dataset (NOT in the repo — must be downloaded)
Per the lab spec, the dataset is **not committed** and is git-ignored. The notebook expects it at:

```
Chinese_MNIST_Dataset/
├── chinese_mnist.csv
└── data/            # input_{suite_id}_{sample_id}_{code}.jpg  (15,000 files, flat)
```

To fetch it (a public GitHub mirror bundles the same Kaggle data), run from the repo root:

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone --depth 1 https://github.com/CoderSerio/chinese-mnist.git /tmp/chinese-mnist
mkdir -p Chinese_MNIST_Dataset/data
cp /tmp/chinese-mnist/dataset/chinese_mnist.csv Chinese_MNIST_Dataset/chinese_mnist.csv
cp /tmp/chinese-mnist/dataset/data/data/input_*.jpg Chinese_MNIST_Dataset/data/
```

Note the images in the mirror live under `dataset/data/data/` (double `data`); the notebook's `image_dir` points to a **flat** `Chinese_MNIST_Dataset/data/`, so copy the jpgs directly into it as above. The original Kaggle source is https://www.kaggle.com/datasets/gpreda/chinese-mnist (requires a Kaggle account/token).

### Run / execute the notebook
Open interactively:

```bash
python3 -m jupyter notebook COMP9517_Lab3.ipynb
```

Re-execute all cells headless (writes outputs back into the file; the spec requires all cells to be executed):

```bash
python3 -m jupyter nbconvert --to notebook --execute --inplace \
  --ExecutePreprocessor.timeout=1200 --ExecutePreprocessor.kernel_name=python3 \
  COMP9517_Lab3.ipynb
```

Full execution takes ~1.5–2 minutes; the SGD classifier is the slowest step (roughly a minute at 10,000 training images). There is no separate build/lint/test setup for this repo.
