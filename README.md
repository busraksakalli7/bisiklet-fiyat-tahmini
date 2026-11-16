# 🚲 Bisiklet Fiyat Tahmini (Yapay Sinir Ağı ile Regresyon)

Bisikletin iki özelliğine (`BisikletOzellik1`, `BisikletOzellik2`) bakarak **fiyatını tahmin eden** basit bir yapay sinir ağı projesi. TensorFlow/Keras ile yazılmıştır ve regresyon problemine giriş niteliğindedir.

## 📌 Proje Özeti

- **Veri seti:** `bisiklet_fiyatlari.xlsx` (1000 satır; `Fiyat`, `BisikletOzellik1`, `BisikletOzellik2`)
- **Hedef (label):** `Fiyat`
- **Girdiler (feature):** `BisikletOzellik1`, `BisikletOzellik2`
- **Model:** Keras `Sequential` – 3 gizli katman (4 nöron, ReLU) + 1 çıkış nöronu
- **Kayıp fonksiyonu:** MSE, **optimizer:** RMSprop, **epoch:** 250

## 🔄 Adımlar

1. Veri `pandas` ile Excel'den okunur.
2. `seaborn.pairplot` ile veri görselleştirilir.
3. Veri %67 eğitim / %33 test olarak ayrılır (`random_state=15`).
4. `MinMaxScaler` ile özellikler 0-1 aralığına ölçeklenir (scaler yalnızca eğitim verisine `fit` edilir).
5. Model eğitilir ve kayıp grafiği çizilir.
6. Test verisi üzerinde tahmin yapılır, gerçek ve tahmin değerleri karşılaştırılır.
7. Eğitilen model `bisiklet_modeli.h5` olarak kaydedilir ve tekrar yüklenip kullanılabilir.

## 📊 Sonuçlar

| Metrik | Değer |
|---|---|
| Eğitim MSE | ~81.5 |
| Test MSE | ~85.6 |
| Test MAE | ~7.4 |

Eğitim ve test hatalarının birbirine yakın olması, modelin aşırı öğrenmediğini (overfitting) gösterir.

## 🛠️ Kurulum

```bash
# Depoyu klonla
git clone https://github.com/KULLANICI_ADIN/bisiklet-fiyat-tahmini.git
cd bisiklet-fiyat-tahmini

# Sanal ortam oluştur (önerilir)
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# Gerekli kütüphaneleri yükle
pip install -r requirements.txt

# Notebook'u aç
jupyter notebook bisiklet_fiyati_tahmin.ipynb
```

## 🔮 Kayıtlı Modeli Kullanma

```python
from tensorflow.keras.models import load_model

model = load_model("bisiklet_modeli.h5")

# Yeni verileri, eğitimde kullandığın scaler ile ölçeklemeyi unutma
yeni = scaler.transform([[1753, 1751]])
print(model.predict(yeni))
```

## 📁 Dosya Yapısı

```
├── bisiklet_fiyati_tahmin.ipynb   # Ana notebook
├── bisiklet_fiyatlari.xlsx        # Veri seti
├── bisiklet_modeli.h5             # Eğitilmiş model
├── requirements.txt               # Bağımlılıklar
└── README.md
```

## 🧰 Kullanılan Teknolojiler

Python · NumPy · Pandas · Seaborn · Matplotlib · scikit-learn · TensorFlow/Keras

## 📝 Notlar

Bu proje öğrenme amaçlıdır. Veri seti sentetik/örnek veridir; gerçek dünya fiyatlarını yansıtmaz.
