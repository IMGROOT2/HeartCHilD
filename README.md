# HeartCHilD: Pediatric CHD Screening via 1D-CNN Ensemble

An end‑to‑end pipeline for congenital heart disease (CHD) screening in children using 12‑lead ECGs. HeartCHilD integrates structured windowing, targeted augmentation, balanced weighting, model ensembling, and probability calibration to achieve high discrimination and reliable risk scores on limited pediatric data.

## Main Features

- **Group-aware Windowing**  
  Splits 12-lead ECGs into disjoint 2-second windows, ensuring patient-exclusive train/test folds.

- **Targeted Data Augmentation**  
  • 50% overlap cropping to expand training windows  
  • Additive Gaussian noise N(0, 0.01) to enhance robustness

- **Balanced Class Weighting**  
  Mitigates normal/arrhythmic imbalance in the loss function.

- **Ensemble Learning**  
  5-fold GroupKFold models averaged for stable predictions.

- **Probability Calibration**  
  Isotonic regression on held-out windows yields well-calibrated risk scores.

## Project Structure

```
research/
├── README.md                      ← this file
├── HeartCHilD.ipynb               ← end-to-end pipeline
├── requirements.txt               ← package dependencies
├── data/
    └── PhysioNet-Leipzig/         ← Leipzig 12-lead ECGs <- Import the folder into data/ here.

```

## Performance

**Window-Level (5-Fold CV)**:
- AUC: **0.95 ± 0.04**
- Accuracy: 0.88 ± 0.09
- Sensitivity: 0.94 ± 0.04

**Patient-Level**:
- AUC: **0.95** (95% CI: [0.86, 1.00])
- Sensitivity: 0.89
- Specificity: 0.83

**Dataset**: 39 patients (29 pediatric CHD, 10 adult controls), 17,145 windows, 113,924 annotated beats

## Running HeartCHilD

1. **Requirements**: Python 3.10+

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Download dataset**:  
   Place [Leipzig Heart Center ECG Database](https://physionet.org/content/ecg-leipzig-arrhythmias-chd/1.0.0/) in `data/PhysioNet-Leipzig/`

4. **Run pipeline**:  
   Open and execute all cells in `HeartCHilD.ipynb`

## Key Results

- **Overlap Validation**: Tested 0%, 25%, 50% overlap strategies (p=0.21, no significant difference)
- **Calibration**: Brier score improved from 0.0945 → 0.0819 after isotonic regression (13.4% reduction)
- **Fold Consistency**: Individual fold AUCs: 0.880, 0.967, 0.989, 0.955, 0.964

## References & Acknowledgments

Thanks to S. Klehs _et al._ for their impressive work at the Leipzig Heart Center, and to the PhysioNet team for maintaining open medical datasets. Thanks to the developers of TensorFlow, scikit-learn, WFDB, and all packages used in this research.
