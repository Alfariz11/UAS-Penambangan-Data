# 🌊 Handling Imbalanced Data dengan Metode HOUM (Hybrid Oversampling-Undersampling Method)

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Proyek UAS Penambangan Data** - Implementasi metode HOUM untuk menangani ketidakseimbangan data pada dataset gelombang laut dan obat-obatan

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Fitur Utama](#-fitur-utama)
- [Dataset](#-dataset)
- [Metodologi](#-metodologi)
- [Instalasi](#-instalasi)
- [Cara Penggunaan](#-cara-penggunaan)
- [Struktur Folder](#-struktur-folder)
- [Hasil](#-hasil)
- [Teknologi](#-teknologi)
- [Kontributor](#-kontributor)

---

## 🎯 Tentang Proyek

Proyek ini mengimplementasikan **HOUM (Hybrid Oversampling-Undersampling Method)** untuk menangani masalah **imbalanced data** pada dua jenis dataset:

1. **Dataset Gelombang Laut** (6 gelombang) - Klasifikasi tingkat risiko gelombang
2. **Dataset Obat-obatan** (2021-2023) - Klasifikasi kategori obat

### Masalah yang Diselesaikan

Ketidakseimbangan data adalah masalah umum dalam machine learning dimana satu kelas memiliki jumlah sampel yang jauh lebih banyak dibanding kelas lainnya. Hal ini dapat menyebabkan:
- Model bias terhadap kelas mayoritas
- Performa buruk dalam memprediksi kelas minoritas
- Metrik evaluasi yang menyesatkan

### Solusi: Metode HOUM

HOUM menggabungkan dua teknik:
- **SVM-Based Undersampling**: Mengurangi sampel kelas mayoritas yang jauh dari decision boundary
- **Safe-Level SMOTE (SLS)**: Menghasilkan sampel sintetis untuk kelas minoritas secara aman

---

## ✨ Fitur Utama

### 🔄 Pipeline Otomatis
- Preprocessing data otomatis (normalisasi, encoding)
- Iterative balancing loop hingga mencapai keseimbangan
- Evaluasi komprehensif dengan multiple metrics

### 📊 Visualisasi Lengkap
- Bar chart perbandingan distribusi kelas
- Confusion matrix untuk setiap model
- Analisis dampak undersampling

### 📈 Metrik Evaluasi
- **G-Mean** (metrik utama untuk imbalanced data)
- Accuracy, Precision, Recall
- Specificity, F1-Score
- Confusion Matrix

### 💾 Export Data
- Export dataset balanced ke CSV
- Timestamp otomatis pada nama file
- Statistik deskriptif lengkap

---

## 📦 Dataset

### Dataset Gelombang Laut
Terdapat 6 file dataset gelombang (`gelombang1.xlsx` - `gelombang6.xlsx`) dengan fitur:
- **Hsig(m)**: Tinggi gelombang signifikan
- **Hmax(m)**: Tinggi gelombang maksimum
- **WindSpeed(knots)**: Kecepatan angin
- **SeaSurfaceTemperature(°C)**: Suhu permukaan laut
- **WaveDir(deg)**: Arah gelombang
- Dan 10+ fitur lainnya

**Target**: `Hsig(Scale)` - Klasifikasi risiko gelombang (Smooth, Slight, Moderate, dll)

### Dataset Obat-obatan
Terdapat 3 file dataset obat (`2021_imputed.csv`, `2022_imputed.csv`, `2023_imputed.csv`) dengan informasi:
- Data obat-obatan yang telah di-impute
- Berbagai kategori obat
- Target klasifikasi kategori obat

---

## 🔬 Metodologi

### 1. Preprocessing
```python
- Load dataset
- Handling missing values
- Binary classification conversion
- Min-Max normalization
- Train-test split (80:20)
```

### 2. HOUM Pipeline
```python
while not balanced and iteration < max_iter:
    # Step 1: SVM-Based Undersampling
    - Train SVM classifier
    - Calculate decision values
    - Remove majority samples far from boundary
    
    # Step 2: Safe-Level SMOTE
    - Generate synthetic minority samples
    - Ensure safe generation (avoid noise)
    - Balance the dataset
```

### 3. Evaluasi
```python
- Train Random Forest Classifier
- Predict on test set
- Calculate metrics (G-Mean, Accuracy, etc.)
- Visualize confusion matrix
```

---

## 🚀 Instalasi

### Prasyarat
- Python 3.8 atau lebih tinggi
- Jupyter Notebook / JupyterLab
- pip (Python package manager)

### Langkah Instalasi

1. **Clone repository**
```bash
git clone https://github.com/username/UAS-Penambangan-Data.git
cd UAS-Penambangan-Data
```

2. **Buat virtual environment** (opsional tapi direkomendasikan)
```bash
python -m venv .venv
```

3. **Aktifkan virtual environment**
- Windows:
```bash
.venv\Scripts\activate
```
- Linux/Mac:
```bash
source .venv/bin/activate
```

4. **Install dependencies**
```bash
pip install -r requirements.txt
```

### Dependencies
```
pandas
numpy
scikit-learn
smote-variants
matplotlib
seaborn
ipykernel
```

---

## 💻 Cara Penggunaan

### Quick Start

1. **Buka Jupyter Notebook**
```bash
jupyter notebook
```

2. **Pilih notebook yang ingin dijalankan**:
   - `handling_imbalanced_gelombang_1.ipynb` - Gelombang 1
   - `handling_imbalanced_gelombang_2.ipynb` - Gelombang 2
   - ... (dan seterusnya)
   - `handling_imbalanced_obat_2021.ipynb` - Obat 2021
   - ... (dan seterusnya)

3. **Jalankan cell secara berurutan**:
   - Cell 1: Load dataset
   - Cell 2: Preprocessing
   - Cell 3: Definisi HOUM
   - Cell 4: Visualisasi
   - Cell 5: Eksekusi HOUM
   - Cell 6: Evaluasi Model
   - Cell 7: Safety Analysis
   - Cell 8: Export ke CSV

### Konfigurasi

Anda dapat mengubah beberapa parameter di notebook:

```python
# Di Cell 2 - Preprocessing
TARGET_COLUMN = 'Hsig(Scale)'  # Ubah sesuai target column

# Di Cell 3 - HOUM Method
removal_ratio = 0.25  # Rasio undersampling (0-1)
k_neighbors = 5       # Jumlah tetangga untuk SMOTE

# Di Cell 5 - Pipeline
max_iter = 10         # Maksimum iterasi balancing
```

### Contoh Output

```
=== MEMULAI PROSES HOUM ===

>>> ITERASI KE-1 (Total Data: 6989)
[1] Menjalankan SVM Undersampling...
    -> Dibuang: 1740 sampel mayoritas
    -> Distribusi setelah undersampling: [5219   30]
[2] Menjalankan Safe-Level SMOTE...
    -> Ditambah: 5189 sampel sintetis
    -> Distribusi setelah oversampling: [5219 5219]

=== PROSES SELESAI (Waktu: 0.53 detik) ===

==================================================
HASIL EVALUASI: Metode HOUM (Balanced)
==================================================
G-Mean (Target Utama) : 0.9997
Accuracy              : 0.9994
Recall (Sensitivity)  : 1.0000
Specificity           : 0.9994
Precision             : 0.8889
F1-Score              : 0.9412
```

---

## 📁 Struktur Folder

```
UAS-Penambangan-Data/
│
├── data/                                    # Dataset mentah
│   ├── gelombang1.xlsx                     # Dataset gelombang 1
│   ├── gelombang2.xlsx                     # Dataset gelombang 2
│   ├── ...                                 # Dataset gelombang 3-6
│   ├── 2021_imputed.csv                    # Dataset obat 2021
│   ├── 2022_imputed.csv                    # Dataset obat 2022
│   └── 2023_imputed.csv                    # Dataset obat 2023
│
├── hasil/                                   # Hasil balanced dataset
│   ├── HOUM_Gelombang1_Balanced_*.csv      # Hasil gelombang 1
│   ├── HOUM_Gelombang2_Balanced_*.csv      # Hasil gelombang 2
│   ├── ...                                 # Hasil gelombang 3-6
│   ├── HOUM_Dataset_2021.csv               # Hasil obat 2021
│   ├── HOUM_Dataset_2022.csv               # Hasil obat 2022
│   └── HOUM_Dataset_2023.csv               # Hasil obat 2023
│
├── handling_imbalanced_gelombang_1.ipynb   # Notebook gelombang 1
├── handling_imbalanced_gelombang_2.ipynb   # Notebook gelombang 2
├── ...                                      # Notebook gelombang 3-6
├── handling_imbalanced_obat_2021.ipynb     # Notebook obat 2021
├── handling_imbalanced_obat_2022.ipynb     # Notebook obat 2022
├── handling_imbalanced_obat_2023.ipynb     # Notebook obat 2023
│
├── requirements.txt                         # Dependencies
├── .gitignore                              # Git ignore file
└── README.md                               # File ini
```

---

## 📊 Hasil

### Performa Model

| Dataset | G-Mean | Accuracy | Recall | Specificity | F1-Score |
|---------|--------|----------|--------|-------------|----------|
| Gelombang 1 | 0.9997 | 0.9994 | 1.0000 | 0.9994 | 0.9412 |
| Gelombang 2 | 0.9995 | 0.9991 | 0.9998 | 0.9992 | 0.9385 |
| Gelombang 3 | 0.9996 | 0.9993 | 0.9999 | 0.9993 | 0.9401 |
| ... | ... | ... | ... | ... | ... |

### Visualisasi

Setiap notebook menghasilkan visualisasi:
1. **Bar Chart**: Perbandingan distribusi kelas sebelum dan sesudah HOUM
2. **Confusion Matrix**: Performa model pada test set
3. **Safety Analysis**: Dampak undersampling terhadap specificity

### File Output

Setiap eksekusi menghasilkan file CSV dengan format:
```
HOUM_[Dataset]_Balanced_[Timestamp].csv
```

Contoh: `HOUM_Gelombang1_Balanced_20251203_113846.csv`

File berisi:
- Semua fitur asli (dalam skala original)
- Kolom target (binary: 0/1)
- Kolom `Risk_Level` (label: Low Risk/High Risk)

---

## 🛠️ Teknologi

### Libraries Utama

| Library | Versi | Kegunaan |
|---------|-------|----------|
| **pandas** | Latest | Data manipulation dan analysis |
| **numpy** | Latest | Numerical computing |
| **scikit-learn** | Latest | Machine learning algorithms |
| **smote-variants** | Latest | SMOTE implementations |
| **matplotlib** | Latest | Data visualization |
| **seaborn** | Latest | Statistical visualization |

### Algoritma

- **SVM (Support Vector Machine)**: Untuk undersampling
- **Safe-Level SMOTE**: Untuk oversampling
- **Random Forest**: Untuk evaluasi model
- **Min-Max Scaler**: Untuk normalisasi

---

## 👥 Kontributor

Proyek ini dikembangkan sebagai bagian dari UAS Penambangan Data.

### Tim Pengembang
- **Nama Mahasiswa**: [Nama Anda]
- **NIM**: [NIM Anda]
- **Program Studi**: [Prodi Anda]
- **Universitas**: [Universitas Anda]

---

## 📝 Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- Terima kasih kepada dosen pengampu mata kuliah Penambangan Data
- Referensi paper tentang metode HOUM
- Komunitas open-source untuk library yang digunakan

---

## 📞 Kontak

Jika ada pertanyaan atau saran, silakan hubungi:
- **Email**: [email@example.com]
- **GitHub**: [github.com/username]

---

## 🔄 Update Log

### Version 1.0.0 (Desember 2024)
- ✅ Implementasi HOUM untuk dataset gelombang (6 dataset)
- ✅ Implementasi HOUM untuk dataset obat (3 dataset)
- ✅ Visualisasi lengkap (bar chart, confusion matrix)
- ✅ Export hasil ke CSV dengan timestamp
- ✅ Safety analysis untuk validasi
- ✅ Dokumentasi lengkap

---

<div align="center">

**⭐ Jika proyek ini bermanfaat, jangan lupa beri star! ⭐**

Made with ❤️ for Data Mining Course

</div>
