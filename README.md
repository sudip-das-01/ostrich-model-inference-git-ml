# ostrich-model-inference-git-ml — Iris Dataset (main branch)

This branch contains a trained scikit-learn classification model for the classic **Iris** dataset. It is used as a reference repository for the Ostrich `git` inference type.

## Repository Structure

```
.
├── dataset/
│   └── input.csv          # Input features (150 samples, no target column)
├── model/
│   └── model.pkl          # Trained scikit-learn classifier (pickle)
├── inference.py           # Inference entrypoint
├── schema.json            # Required input feature column names
├── requirements.txt       # Python dependencies
└── Dockerfile             # Container definition
```

## Input Features

Defined in `schema.json` under `input_parameters_name`:

| Feature | Description |
|---|---|
| `sepal length (cm)` | Sepal length in centimetres |
| `sepal width (cm)` | Sepal width in centimetres |
| `petal length (cm)` | Petal length in centimetres |
| `petal width (cm)` | Petal width in centimetres |

## Output

Running inference produces `output/output.csv` with a single `target` column containing predicted class labels (0 = Setosa, 1 = Versicolour, 2 = Virginica).

## Running Locally

```bash
pip install -r requirements.txt
python inference.py
# output written to output/output.csv
```

## Running with Ostrich git Inference Generator

The Ostrich inference generator can generate an `inference.py` that clones this repo to a temp directory, reads `dataset/input.csv`, validates features via `schema.json`, runs predictions, and pushes `output/output.csv` back:

```bash
python inference_py_generator.py \
  --payload-json sample_payload_git.json \
  --repo-type git
```

The generated script accepts:
- `--repo-url` — GitHub repo URL (default: this repo)
- `--branch` — branch name (default: `main`)
- `--output` — output CSV path (default: `output/output.csv`)
