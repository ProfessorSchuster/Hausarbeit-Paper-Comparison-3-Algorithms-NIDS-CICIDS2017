# Comparison of an established supervised and an unsupervised machine learning model with a novel self-supervised framework for network anomaly detection using the CIC-IDS2017 dataset

_Note: The paper is uploaded in this GitHub Repository._

## Abstract
This paper investigates the application of machine learning for anomaly-based intrusion detection systems using the CIC-IDS2017 dataset. Three representative approaches are implemented and compared: a supervised Random Forest, an unsupervised Isolation Forest, and the recent Encrypted Traffic Self-Supervised Learning framework (ET-SSL). The experiment evaluates each model under a standard closed-set scenario and a zero-day setting, where selected attack classes are withheld during training. Results show that the Random Forest achieves near-perfect discrimination with macro F1-scores above 0.99 and minimal false-alarm rates, confirming and surpassing related work through optimized preprocessing and threshold tuning. ET-SSL demonstrates moderate but robust performance, generalizing to unseen attacks better than the Isolation Forest, though it remains below state-of-the-art deep autoencoder frameworks. The Isolation Forest consistently underperforms, missing more than half of malicious traffic due to violated assumptions about anomaly rarity. These findings suggest that supervised ensemble methods remain highly effective for datasets such as CIC-IDS2017, while self-supervised frameworks like ET-SSL offer promising avenues for adaptive detection in evolving network environments.

## Repository Structure
```
notebooks/ # Jupyter notebooks
│ ├── 00_read_csv.ipynb # Read + clean raw CSVs
│ ├── 01_preprocess_cicids.ipynb # Preprocess & build splits
│ ├── 02_train_models.ipynb # Train RF, IF, ET-SSL (base & zero-day)
│ └── 03_evaluate_models.ipynb # Evaluate + plots, metrics, confusion matrices
requirements.txt # Python dependencies
README.md # This file
Hausarbeit_Cedric-Schuster.pdf # final paper
```

## Workflow
Note: This repository contains only the Jupyter Notebooks to rebuild the dataset, pre-process it, train the models and evaluate them. Due to their size, no models or datasets were uploaded to this repository.

### 00 — Read CSV
- Combine the raw **CIC-IDS2017** CSVs into a single cleaned Parquet file.
- Handles missing values, column normalization, label unification.

### 01 — Preprocess CICIDS
- Drop missing / categorical / constant features.
- Normalize with MinMaxScaler.
- Build 70/15/15 splits:
  - RF: stratified, benign + malicious.
  - IF: train on benign only.
  - ET-SSL: train with benign + malicious.
- Build zero-day scenario: remove Bot, Web Attack - Brute Force, Infiltration from train/val.

### 02 — Train Models
- Train RandomForest (supervised), IsolationForest (unsupervised), and ET-SSL (self-supervised).
- Scenarios: base vs. zero-day.
- Save trained models + thresholds.

### 03 — Evaluate Models
- Load trained models and evaluate on val/test splits.
- Compute confusion matrices, ROC, PR, macro-F1, accuracy, and AUCs.
- Export metrics and figures.

## Installation

Clone the repository and install dependencies. Consider using a venv.

```bash
git clone https://github.com/ProfessorSchuster/Hausarbeit-Paper-Comparison-3-Algorithms-NIDS-CICIDS2017.git

cd Hausarbeit-Paper-Comparison-3-Algorithms-NIDS-CICIDS2017

pip install -r requirements.txt
````

## Dataset
This project uses the CIC-IDS2017 dataset.

Due to size, no raw, pre-processed or split datasets are available in this repository.

If you want to regenerate from raw CSVs, place them in data/raw/ and run 00_read_csv.ipynb.
If you use this repository, please cite the CIC-IDS2017 dataset and the related paper:

```
@misc{CICIDS2017,
 author = {{Canadian Institute for Cybersecurity}},
 year = {2018},
 title = {Intrusion detection evaluation dataset (CIC-IDS2017)},
 url = {https://www.unb.ca/cic/datasets/ids-2017.html}
}

@inproceedings{Sharafaldin.2018,
 author = {Sharafaldin, Iman and {Habibi Lashkari}, Arash and Ghorbani, Ali A.},
 title = {Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization},
 pages = {108--116},
 publisher = {{SCITEPRESS - Science and Technology Publications}},
 isbn = {978-989-758-282-0},
 booktitle = {Proceedings of the 4th International Conference on Information Systems Security and Privacy},
 year = {2018},
 doi = {10.5220/0006639801080116}
}
```

## License
This repository is for academic purposes. Please check dataset license before redistribution.