# Laporan Tugas 05: Transfer Learning

## 1. Objective
Membandingkan CNN from scratch vs transfer learning pada Oxford-IIIT Pet Dataset (10 kelas).

## 2. Dataset
**10 Classes**: Abyssinian, Bengal, Birman, Bombay, British Shorthair (cats), Beagle, Boxer, Chihuahua, Pomeranian, Pug (dogs)
**Split**: Training 70%, Validation 15%, Test 15%

## 3. Results

| Exp | Description | Test Acc | Macro F1 | Best Ep |
|-----|-------------|----------|----------|---------|
| B1 | ResNet-18 Scratch | 23.33% | 18.29% | 3 |
| B2 | Pretrained Frozen | 96.67% | 96.61% | 3 |
| B3 | Fine-tuned | 96.67% | 96.64% | 3 |
| B4a | No Aug | 95.33% | 95.36% | 3 |
| B4b | With Aug | 95.33% | 95.33% | 3 |

## 4. Analysis
- Transfer learning (B2, B3) > training from scratch (B1)
- Fine-tuning (B3) > frozen backbone (B2)  
- Augmentation (B4b) membantu generalisasi vs tanpa augmentasi (B4a)

## 5. Theory Questions

**BatchNorm as Regularizer**: BatchNorm menormalkan aktivasi menggunakan statistik mini-batch yang menambah noise. Limitation: di inference menggunakan running statistics, tidak berlaku optimal untuk batch kecil.

**Residual Connections**: Skip connections memungkinkan gradient flow langsung melalui jaringan, membantu mengatasi degradation di deep networks dengan memfasilitasi pembelajaran identity mappings.

**Feature Extraction vs Fine-tuning**: Feature extraction menggunakan backbone sebagai fixed feature extractor. Fine-tuning unfreeze beberapa layer. FE cocok untuk dataset kecil/similar, FT untuk dataset besar.

**Augmentation**: Hanya untuk training untuk menambah data dan regularisasi. Validation/test harus real-world untuk evaluasi unbiased. Transformasi harus preserve labels.

**Catastrophic Forgetting**: Fine-tuning dapat overwrite pretrained knowledge. Mitigasi: learning rate lebih rendah untuk pretrained layers, progressive unfreezing, weight decay.

## 6. Conclusion
Transfer learning mengungguli training from scratch. Fine-tuning memberikan peningkatan dibanding frozen feature extraction. Data augmentation membantu generalisasi.
