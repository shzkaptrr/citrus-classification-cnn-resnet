# 🍊 Comparative Analysis: CNN vs ResNet50 for Citrus Classification

Project ini bertujuan untuk membandingkan performa arsitektur **CNN from Scratch** dengan **Transfer Learning (ResNet50)** dalam mengklasifikasikan 3 jenis jeruk lokal yang memiliki kemiripan visual tinggi: **Jeruk Nipis, Jeruk Purut, dan Jeruk Limau**.

---

## 📌 Project Overview

Membedakan jenis jeruk secara visual bisa menjadi tantangan karena kemiripan warna dan bentuk. Perbedaan utama terletak pada tekstur kulit (pori-pori). Project ini mengeksplorasi tiga pendekatan:

1. **Baseline:** Membangun CNN sederhana dari nol (*scratch*).
2. **Transfer Learning:** Menggunakan ResNet50 sebagai *Feature Extractor* (tanpa augmentasi data).
3. **Fine-Tuning:** Melatih ulang layer ResNet50 untuk melihat efek pada dataset kecil tanpa augmentasi.

---

## 📂 Dataset

Dataset dikumpulkan secara mandiri (*Custom Dataset*) baik melalui teknik *web scraping* maupun download manual dari berbagai sumber (Google Images, Shutterstock, E-Commerce, dll) dan dibersihkan secara manual.

* **Total Citra:** 1.002 Gambar.
* **Distribusi:** Seimbang (*Balanced*), ~334 gambar per kelas.
* **Kelas:**
* `Jeruk Nipis` (Tekstur halus, kulit tipis).
* `Jeruk Purut` (Tekstur kasar/keriput, kulit tebal).
* `Jeruk Limau` (Tekstur berpori sedang, ukuran kecil).



---

## ⚙️ Methodology & Experiments

### Scenario 1: Custom CNN (From Scratch)

* **Arsitektur:** 4 Blok Konvolusi (Conv2D + MaxPool) + Fully Connected Layer.
* **Tujuan:** Menetapkan *baseline* akurasi tanpa bantuan model pre-trained.

### Scenario 2: Transfer Learning (ResNet50) 🏆

* **Arsitektur:** ResNet50 (ImageNet Weights) + GlobalAveragePooling + Custom Dense Head.
* **Strategi:** *Freeze* semua layer ResNet, hanya melatih layer klasifikasi.
* **Fitur:** Menggunakan `ReduceLROnPlateau` untuk optimasi learning rate.

### Scenario 3: Fine-Tuning (Ablation Study)

* **Strategi:** *Unfreeze* 30 layer terakhir ResNet50.
* **Kondisi:** Tanpa Data Augmentation (Hanya rescaling).
* **Tujuan:** Menguji sensitivitas model kompleks terhadap risiko *overfitting* pada data terbatas.

---

## 📊 Results & Analysis
1. CNN from scratch
<img width="656" height="535" alt="image" src="https://github.com/user-attachments/assets/af64adf6-46db-4d1a-b84f-7a7caf682857" />

2. Resnet + Praproses
<img width="596" height="523" alt="image" src="https://github.com/user-attachments/assets/40906b0a-d01c-427d-8a82-61827a22eb1b" />

3. Resnet Tanpa Praproses
<img width="712" height="586" alt="image" src="https://github.com/user-attachments/assets/a400c4f7-98bc-4613-b8b6-276fe07b7129" />


Berikut adalah perbandingan performa dari ketiga skenario:

| Model | Metode | Akurasi Validasi | Loss | Status |
| --- | --- | --- | --- | --- |
| **Custom CNN** | Scratch | 61.11% | Tinggi (>1.0) | Underfitting |
| **ResNet50** | **Transfer Learning** | **88.38%** | **Rendah (<0.1)** | **Best Performance** 🥇 |
| **ResNet50** | Fine-Tuning (No Aug) | 64.65% | Sangat Tinggi | Overfitting |

### 📈 Visualisasi Hasil (Champion Model)

### 💡 Key Insights

1. **Transfer Learning Juara:** ResNet50 mampu mengekstraksi fitur tekstur jeruk dengan sangat baik meski data terbatas, mengatasi masalah *underfitting* pada model Scratch.
2. **Pentingnya Augmentasi:** Pada Skenario 3, *Fine-Tuning* tanpa augmentasi menyebabkan akurasi turun drastis dan loss meledak. Ini membuktikan bahwa untuk model kompleks, variasi data (augmentasi) adalah hal wajib untuk mencegah *memorization/overfitting*.

---

## 🛠️ Tech Stack

* **Language:** Python 3.x
* **Framework:** TensorFlow / Keras
* **Libraries:** NumPy, Matplotlib, Seaborn, Scikit-learn, PIL.
* **Tools:** Google Colab, Google Drive API.

---

## 🚀 How to Run

1. Clone repository ini:
```bash
git clone https://github.com/username-kamu/citrus-classification-cnn-resnet.git

```


2. Install library yang dibutuhkan:
```bash
pip install tensorflow matplotlib seaborn scikit-learn

```


3. Jalankan Notebook (pilih skenario yang diinginkan):
`jupyter notebook` atau upload ke Google Colab.


---
