# Legal Document Generator

An n-gram language model, built from scratch in one Jupyter notebook, that learns from real contracts and writes contract-style text from a short prefix.

The output is a statistical imitation. It reads like a contract for a clause or so, then loses the thread, and it can't be used as a legal document.

## Results

Trained on 1,000 contracts from [`albertvillanova/legal_contracts`](https://huggingface.co/datasets/albertvillanova/legal_contracts), with 100 each for dev and test.

| | |
|---|---|
| Model | 4-gram with Witten-Bell smoothing |
| Vocabulary | 22,618 words, from the train set only |
| Dev perplexity | 38.4 |
| Test perplexity | 33.9 |
| Default prefix | "whereas, the" |

Full metrics and charts are in [`reports/`](reports/).

## Data source

The training data is the [`legal_contracts`](https://huggingface.co/datasets/albertvillanova/legal_contracts) dataset by albertvillanova on Hugging Face, mostly exhibits attached to SEC filings. The notebook downloads it, and this repo doesn't include the raw data. The dataset page states no licence, and the contracts belong to their original parties.

The notebook's saved outputs include short excerpts and generated text that can contain real company and personal names from those filings.

## Run it

Uses Python 3.12.

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m ipykernel install --user --name nlp-generator
jupyter notebook nlp_generator.ipynb
```

Run all cells. The first run downloads about 130 MB of contracts into `data/` and saves the model to `models/` (about 85 MB). Neither folder is in this repo because the notebook rebuilds them.

To change the dataset size or model settings, edit the config cell at the top and re-run. To try your own prefix, use the last cell. Partial words like `intro` work too.
