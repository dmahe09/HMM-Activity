# Modeling Human Activity States Using Hidden Markov Models
### Formative 2 — Hidden Markov Models

This repository infers hidden human-activity states (**standing, walking, jumping, still**)
from smartphone accelerometer and gyroscope signals using a Hidden Markov Model.

## Repository structure

```
HMM_Activity_Recognition/
├── HMM_Activity_Recognition.ipynb   # main notebook (run top-to-bottom)
├── data/                            # labeled sensor recordings
│   ├── standing/   (10 recordings)
│   ├── walking/    (10 recordings)
│   ├── jumping/    (10 recordings)
│   └── still/      (10 recordings)
│       └── <recording>/Accelerometer.csv, Gyroscope.csv, Metadata.csv
├── README.md
└── group-info.pdf                   # <-- add the filled/exported document here
```

## How to run

1. Install dependencies:
   ```
   pip install hmmlearn seaborn scikit-learn pandas numpy matplotlib
   ```
2. Open `HMM_Activity_Recognition.ipynb`.
3. Make sure the `DATA_DIR = "data"` path in Section 1 points to the `data/` folder.
4. Run all cells (Kernel → Restart & Run All).

## Method summary

- **Data:** 40 recordings, iPhone X, Sensor Logger, 100 Hz (10 ms sample rate).
- **Windowing:** 1-second windows (100 samples) with 50% overlap.
- **Features:** 24 per window — time-domain (mean, std, RMS, SMA, axis correlation)
  and frequency-domain (dominant frequency, spectral energy from FFT); Z-score normalized.
- **Model:** 4-state Gaussian HMM, supervised initialization + Baum–Welch training
  (log-likelihood convergence), Viterbi decoding (implemented from scratch, verified
  against `hmmlearn`).
- **Evaluation:** 2 held-out recordings per activity (unseen test set), confusion matrix,
  per-activity sensitivity / specificity / accuracy.

## Result

Overall accuracy on the unseen test set: **~0.98**.
