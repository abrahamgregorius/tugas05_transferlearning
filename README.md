# Tugas 05: Transfer Learning

## Advanced CNNs and Transfer Learning - Oxford-IIIT Pet Classification

**Course:** Deep Learning - Lecture  
**Dataset:** Oxford-IIIT Pet Dataset  
**Objective:** Compare training CNN from scratch vs transfer learning approaches

---

## Experiments

| Experiment | Description | Test Accuracy | Macro F1 |
|------------|-------------|--------------|----------|
| **B1** | ResNet-18 from scratch | 23.33% | 18.29% |
| **B2** | Pretrained + Frozen backbone | 96.67% | 96.61% |
| **B3** | Fine-tuned (layer4 + fc) | 96.67% | 96.64% |
| **B4a** | No augmentation | 95.33% | 95.36% |
| **B4b** | With augmentation | 95.33% | 95.33% |

---

## Project Structure

```
Tugas05_TransferLearning/
├── Tugas05_TransferLearning.ipynb   # Main notebook
├── run_quick.py                     # Quick training script (3 epochs)
├── run_experiments.py               # Full training script (10 epochs)
├── requirements.txt                 # Dependencies
├── README.md                        # This file
├── oxford_pet_dataset/              # Downloaded dataset
└── outputs/
    ├── checkpoints/                 # Saved model weights
    │   ├── model_b1.pth
    │   ├── model_b2.pth
    │   ├── model_b3.pth
    │   ├── model_b4a.pth
    │   └── model_b4b.pth
    ├── histories/                    # Training logs
    │   └── history_*.json
    ├── plots/                       # Generated visualizations
    │   ├── training_curves.png
    │   ├── validation_curves.png
    │   ├── metrics_comparison.png
    │   └── confusion_matrices.png
    ├── misclassified/               # Misclassification analysis
    │   ├── misclassified_examples.png
    │   └── misclassified_info.json
    ├── metrics.csv                  # Results summary
    └── metrics.json                 # Detailed metrics
```

---

## Setup

```bash
pip install -r requirements.txt
```

Requirements:
- Python 3.10+
- PyTorch 2.0+
- torchvision
- scikit-learn
- pandas
- matplotlib
- tqdm
- Pillow

---

## Running the Experiments

### Option 1: Jupyter Notebook
```bash
jupyter notebook Tugas05_TransferLearning.ipynb
```
Run all cells sequentially. The notebook contains:
1. Data loading and preprocessing
2. All 5 experiments (B1-B4b)
3. Evaluation and visualization
4. Report generation

### Option 2: Quick Run (3 epochs, CPU-friendly)
```bash
python run_quick.py
```

### Option 3: Full Run (10 epochs)
```bash
python run_experiments.py
```

---

## Experiment Details

### B1: CNN from Scratch
- ResNet-18 initialized with random weights
- All layers trainable
- Learning rate: 1e-3
-optimizer: AdamW
- Result: Poor performance due to insufficient data for training from scratch

### B2: Pretrained Frozen
- ResNet-18 pretrained on ImageNet
- All backbone layers frozen
- Only classifier (fc) trainable
- Learning rate: 1e-3
- Result: Excellent performance, demonstrating transfer of low-level features

### B3: Fine-tuning
- ResNet-18 pretrained on ImageNet
- Unfrozen layer4 and classifier
- Learning rates: layer4=1e-4, fc=1e-3
- Result: Best performance with task-specific adaptation

### B4: Augmentation Comparison
- **B4a**: No augmentation (Resize + Normalize only)
- **B4b**: Full augmentation (RandomCrop, HorizontalFlip, ColorJitter, Rotation)

---

## Dataset

- **Source:** Oxford-IIIT Pet Dataset (via torchvision)
- **Classes used:** 10 (5 cat breeds + 5 dog breeds)
  - Abyssinian, Bengal, Birman, Bombay, British Shorthair
  - american_bulldog, american_pit_bull_terrier, beagle, boxer, chihuahua
- **Split:** 70% train / 15% validation / 15% test
- **Image size:** 224x224
- **Normalization:** ImageNet mean/std

---

## Key Findings

1. **Transfer learning dramatically outperforms training from scratch** (96.67% vs 23.33%)
2. **Fine-tuning provides marginal improvement** over frozen feature extraction
3. **Data augmentation has minimal impact** in this experiment (possibly due to pretrained features already being robust)
4. **ResNet-18 features transfer well** from ImageNet to Oxford-IIIT Pet dataset

---

## Theory Questions (answered in Laporan_Tugas05.md)

1. How BatchNorm can act as a regularizer and its limitations
2. How residual connections help address degradation in deep networks
3. Feature extraction vs fine-tuning and when each is appropriate
4. Why augmentation is used only for training
5. Catastrophic forgetting and ways to mitigate it during fine-tuning

---

## Report

Full report with methodology, results, analysis, and theory answers: `Laporan_Tugas05.md`

---

## Author

**Student:** [Nama Mahasiswa]  
**NIM:** [NIM]

---

## License

This project is for educational purposes as part of the Deep Learning course assignment.
