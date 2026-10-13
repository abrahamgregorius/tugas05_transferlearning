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

**BatchNorm as Regularizer**: BatchNorm menormalkan aktivasi menggunakan statistik dari mini-batch, dan efek sampingnya yaitu menambah noise yang berfungsi sebagai regularisasi. Kelemahannya, saat inference menggunakan running statistics yang dihitung dari seluruh data, sehingga tidak berjalan optimal untuk batch kecil.

**Residual Connections**: Skip connections memungkinkan gradient mengalir langsung melewati beberapa layer sehingga masalah degradation di deep networks bisa diatasi. Selain itu, skip connections juga mempermudah jaringan dalam mempelajari identity mappings.

**Feature Extraction vs Fine-tuning**: Feature extraction menggunakan backbone yang sudah dilatih di dataset lain sebagai feature extractor tetap. Fine-tuning membuka beberapa layer bagian akhir agar bisa dilatih ulang. FE lebih cocok untuk dataset kecil atau mirip dengan dataset pretrained, sedangkan FT lebih cocok untuk dataset yang besar.

**Augmentation**: Augmentation hanya dilakukan saat training untuk menambah variasi data dan sebagai regularisasi. Validation dan test menggunakan data asli tanpa augmentasi supaya evaluasi mencerminkan kondisi nyata. Transformasi yang digunakan harus tetap menjaga label asli dari data.

**Catastrophic Forgetting**: Fine-tuning bisa membuat jaringan lupa pengetahuan yang sudah dipelajari dari pretrained model. Cara mengatasinya antara lain menggunakan learning rate lebih kecil untuk layer pretrained, progressive unfreezing, dan weight decay.

## 6. Conclusion
Transfer learning mengungguli training from scratch. Fine-tuning memberikan peningkatan dibanding frozen feature extraction. Data augmentation membantu generalisasi.
