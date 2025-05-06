# HeartCHilD: Pediatric CHD Screening via 1D‑CNN Ensemble

An end‑to‑end pipeline for congenital heart disease (CHD) screening in children using 12‑lead ECGs. HeartCHilD integrates structured windowing, targeted augmentation, balanced weighting, model ensembling, and probability calibration to achieve high discrimination and reliable risk scores on limited pediatric data.

## Main Features
- Group‑aware Windowing
Splits 12‑lead ECGs into disjoint 2‑second windows, ensuring patient‑exclusive train/test folds.

- Targeted Data Augmentation
50% overlap cropping to expand rare CHD windows
Additive Gaussian noise to enhance robustness

- Balanced Class Weighting
Mitigates CHD/control imbalance in the loss function.

- Ensemble Learning
5‑fold GroupKFold models averaged for stable predictions.

- Probability Calibration
Isotonic regression on held‑out windows yields well‑calibrated risk scores.

## Project Structure
```
heartchild/
├── README.md                ← this file
├── main.py                  ← end‑to‑end pipeline
├── data/
│   └── PhysioNet-Leipzig/   ← Leipzig 12‑lead pediatric ECGs
└── models/
    └── heartchild.keras     ← trained model artifact
```

## Running HeartCHilD
- Make sure you're on Python 3.8 or higher.
- Place this data: https://physionet.org/content/leipzig-heart-center-ecg/1.0.0/ in `data/PhysioNet-Leipzig`.
- Install dependencies: `pip install numpy pandas wfdb scipy matplotlib tensorflow scikit-learn`
- Then, run all cells in the Jupyter Notebook.

## Conclusion
_HeartCHilD_ demonstrates that carefully designed deep learning can deliver reliable, low‑cost CHD screening for children, paving the way for broader clinical adoption.

## References/Thanks
Thanks to S. Klehs _et al._ for their impressive and impactful work at the Leipzig Heart Center. Thanks to the developers of the packages and programs used to complete this research.
