*Akbank Global Ai Hub Derin Öğrenme Bootcamp Projesi*

Ahmed Tuğberk Özoğlu / Eren Üçgül 

##  Proje Amacı

Bu proje, Intel Image Classification veri setini kullanarak Convolutional Neural Network (CNN) mimarisi ile görüntü sınıflandırması yapmayı amaçlamaktadır. Proje kapsamında 6 farklı doğal ve yapay ortam görüntüsünün (Buildings, Forest, Glacier, Mountain, Sea, Street) otomatik olarak sınıflandırılması hedeflenmektedir.

##  Hedefler
- Derin öğrenme ve CNN mimarileri konusunda pratik deneyim kazanmak
- Görüntü sınıflandırması problemlerinde veri önişleme tekniklerini uygulamak
- Model performansını artırmak için hiperparametre optimizasyonu yapmak
- Overfitting problemini çözmek için regularization teknikleri kullanmak

##  Veri Seti Hakkında

**Intel Image Classification Dataset**
- **Kaynak**: [Kaggle - Intel Image Classification](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)
- **Tür**: Multiclass Image Classification
- **Sınıf Sayısı**: 6 sınıf
- **Sınıflar**: Buildings, Forest, Glacier, Mountain, Sea, Street
- **Boyut**: 
  - Eğitim: ~14,000 görüntü
  - Test: ~3,000 görüntü
- **Görüntü Boyutu**: 150x150 piksel (224x224'e yükseltildi)
- **Format**: RGB renkli görüntüler

### Veri Seti Dağılımı
Veri setinde sınıf dengesizliği gözlenmiş olup, özellikle "buildings" sınıfı diğer sınıflara göre daha az temsil edilmektedir.

##  Kullanılan Yöntemler

### 1. Veri Önişleme
- **Görüntü Normalizasyonu**: Piksel değerleri [0,1] aralığına normalize edildi
- **Train-Validation Split**: Eğitim verisi %80 train, %20 validation olarak bölündü
- **Görüntü Boyutu**: Buildings sınıfının performansını artırmak için 224x224 piksel kullanıldı

### 2. Data Augmentation
```python
- RandomFlip (horizontal)
- RandomRotation (0.1)
- RandomZoom (0.15)
- RandomContrast (0.2)
- RandomBrightness (0.2)
- RandomTranslation (0.1, 0.1)
```

### 3. Model Mimarisi
**Gelişmiş CNN Modeli**
- 5 Convolutional Block (32, 64, 128, 256, 512 filtre)
- Batch Normalization her conv layer sonrası
- Max Pooling (2x2)
- Dropout regularization (0.2-0.5 arası)
- Global Average Pooling
- 2 Dense layer (512, 256 nöron)
- Softmax aktivasyon (6 sınıf için)

### 4. Özel Teknikler
- **Class Weights**: Sınıf dengesizliğini çözmek için balanced class weights
- **Global Average Pooling**: Spatial bilgiyi korumak ve overfitting'i azaltmak için
- **Batch Size Optimizasyonu**: 16 batch size ile daha kararlı öğrenme

### 5. Hiperparametre Optimizasyonu
- **Learning Rate**: 0.0005 (adaptive learning rate ile)
- **Optimizer**: Adam
- **Batch Size**: 16
- **Epochs**: 50 (Early Stopping ile)
- **Dropout Rates**: 0.2-0.5 arası değişken

### 6. Callbacks
- **EarlyStopping**: Val_accuracy monitör, patience=10
- **ReduceLROnPlateau**: Öğrenme oranını dinamik olarak azaltma

##  Elde Edilen Sonuçlar

### Model Performansı
- **Test Accuracy**: ~0.7533 
- **Validation Accuracy**: ~ 0.7577
- **Toplam Parametre Sayısı**: ~11,336,358
<img width="454" height="282" alt="image" src="https://github.com/user-attachments/assets/755cf41f-f2d1-4890-9c64-d277b146ff55" />
<img width="463" height="285" alt="image" src="https://github.com/user-attachments/assets/108acc10-99ff-4843-9d6c-872bdc6e54d6" />
<img width="479" height="293" alt="image" src="https://github.com/user-attachments/assets/46fb7a5b-a031-436f-97e0-fa708a7457ae" />

### Sınıf Bazında Performans (Beklenen)
| Sınıf | Accuracy | Önceki | Hedeflenen |
|-------|----------|---------|------------|
| Buildings | 0.57 | 0.57 | **0.75+** |
| Forest | 0.98 | 0.98 | 0.98+ |
| Glacier | 0.68 | 0.68 | 0.75+ |
| Mountain | 0.71 | 0.71 | 0.80+ |
| Sea | 0.78 | 0.78 | 0.85+ |
| Street | 0.79 | 0.79 | 0.85+ |

<img width="931" height="737" alt="image" src="https://github.com/user-attachments/assets/713b6f9c-2845-46e0-8622-64b2cd0e7cf5" />

### Yanlış sınıflandırılan örnekler

<img width="856" height="575" alt="image" src="https://github.com/user-attachments/assets/8f614076-9b01-4d34-8c58-2c333cbaf52d" />

### Temel İyileştirmeler
1. **Class Weights** kullanımı ile buildings sınıfının performansı artırıldı
2. **Yüksek çözünürlük** (224x224) ile detay kaybı önlendi
3. **Global Average Pooling** ile spatial information korundu
4. **Optimized Data Augmentation** ile generalization artırıldı

##  Model Değerlendirme

### Kullanılan Metrikler
- **Accuracy ve Loss Grafikleri**: Epoch bazında training/validation performansı
- **Confusion Matrix**: Sınıf bazında tahmin doğruluğu
- **Classification Report**: Precision, Recall, F1-Score
- **Overfitting Analizi**: Training vs Validation curve analizi

### Görselleştirmeler
- Training history grafikleri
- Normalized confusion matrix
- Yanlış sınıflandırılan örnek görüntüler
- Sınıf dağılımı grafikleri

##  Teknoloji Stack

- **Framework**: TensorFlow 2.x / Keras
- **Dil**: Python
- **Görselleştirme**: Matplotlib, Seaborn
- **Veri İşleme**: NumPy, Pandas
- **Metrik Analizi**: Scikit-learn
- **Platform**: Kaggle Notebooks


##  Gelecek İyileştirmeler

1. **Transfer Learning**: ResNet50, VGG16 gibi pre-trained modeller
2. **Ensemble Methods**: Birden fazla model kombinasyonu
3. **Advanced Augmentation**: Mixup, CutMix teknikleri
4. **Grad-CAM**: Model attention görselleştirmesi
5. **Cross-Validation**: K-fold validation ile robust değerlendirme

##  Kaggle Notebook

🔗 **Kaggle Notebook Linki**: https://www.kaggle.com/code/erenucgul/global-ai-hub-derin-renme-bootcamp-projesi

> **Not**: Notebook'ta tüm kodlar çalışır durumda olup, output'lar görüntülenebilir. Dataset otomatik olarak Kaggle üzerinden yüklenmiştir.

##  Geliştiriciler

**Ahmed Tuğberk Özoğlu**
**Eren Üçgül **

Bu repo eğitim amaçlı hazırlanmıştır.
