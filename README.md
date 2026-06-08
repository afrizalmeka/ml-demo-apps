# 🤖 ML Demo Apps — Machine Learning Interactive Demo

Tiga aplikasi Streamlit interaktif untuk kelas Machine Learning, dirancang untuk dijalankan di **Google Colab** dengan akses publik via **ngrok tunneling**.

---

## 📦 Isi Proyek

```
ml-demo-apps/
└── ML_Demo_Apps.ipynb    ← Satu notebook berisi semua (setup + 3 app + runner)
```

Saat notebook dijalankan, tiga file app akan dibuat otomatis di Colab:
```
app_timeseries.py         ← App 1: Time Series Forecasting      (port 8501)
app_segmentasi.py         ← App 2: Customer Segmentation        (port 8502)
app_cnn.py                ← App 3: CNN Image Classification     (port 8503)
```

---

## 🚀 Cara Menjalankan di Google Colab

### Prasyarat
- Akun Google (untuk Colab)
- Akun ngrok gratis → [daftar di ngrok.com](https://ngrok.com)

### Langkah-langkah

**1. Upload Notebook**
- Buka [colab.research.google.com](https://colab.research.google.com)
- Klik **File → Upload notebook**
- Upload file `ML_Demo_Apps.ipynb`

**2. Dapatkan Ngrok Token**
- Login ke [dashboard.ngrok.com/get-started/your-authtoken](https://dashboard.ngrok.com/get-started/your-authtoken)
- Copy authtoken Anda

**3. Jalankan Cell Secara Berurutan**

| Cell | Aksi | Keterangan |
|------|------|------------|
| **Cell 1** | ▶ Jalankan | Install semua dependencies (~2-3 menit) |
| **Cell 2** | Edit token lalu ▶ | Ganti `YOUR_NGROK_AUTHTOKEN_HERE` dengan token Anda |
| **Cell 3** | ▶ Jalankan | Membuat file `app_timeseries.py` |
| **Cell 4** | ▶ Jalankan | Membuat file `app_segmentasi.py` |
| **Cell 5** | ▶ Jalankan | Membuat file `app_cnn.py` |
| **Cell 6** | ▶ Jalankan | Menjalankan App 1 → klik URL yang muncul |
| **Cell 7** | ▶ Jalankan | Menjalankan App 2 → klik URL yang muncul |
| **Cell 8** | ▶ Jalankan | Menjalankan App 3 → klik URL yang muncul |
| **Cell 9** | *(Opsional)* | Menghentikan semua tunnel ngrok |

**4. Buka Aplikasi**

Setelah cell runner dijalankan, output akan tampil seperti ini:
```
=======================================================
🔮 TIME SERIES FORECASTING APP — SIAP DIGUNAKAN
🌐 Buka di browser: https://xxxx-xxxx.ngrok-free.app
=======================================================
```
Klik URL tersebut → aplikasi terbuka di tab browser baru.

---

## 🔮 App 1: Time Series Forecasting

**File:** `app_timeseries.py` | **Port:** `8501`

Demo peramalan deret waktu menggunakan pendekatan **Supervised Learning dengan Lag Features**.

### Sumber Data (pilih satu)
| Opsi | Deskripsi |
|------|-----------|
| 📊 Data Demo | 36 bulan penjualan sintetis dengan tren, seasonal, noise, dan anomali |
| 📈 Data Saham Live | Fetch harga saham via yfinance (contoh: `BBCA.JK`, `AAPL`, `TSLA`) |
| 📁 Upload CSV | Upload CSV dengan kolom tanggal dan nilai numerik sendiri |

### Format CSV Upload (App 1)
```
tanggal,penjualan
2022-01,120.50
2022-02,115.30
2022-03,130.80
...
```
- Kolom tanggal: format `YYYY-MM` atau `YYYY-MM-DD`
- Minimal 10 baris data
- Setelah upload, pilih mana kolom tanggal dan mana kolom nilai

### Parameter Model (Sidebar)
| Parameter | Range | Default | Keterangan |
|-----------|-------|---------|------------|
| Model | - | Linear Regression | Pilih: Linear / Ridge / Decision Tree |
| Lag Features | 1–12 | 3 | Jumlah nilai historis sebagai fitur input |
| Periode Forecast | 1–12 | 6 | Jumlah periode ke depan yang diramalkan |

### Tabs
- **📈 Data & Prediksi** — Chart interaktif train/test/prediksi/forecast + tabel forecast
- **📊 Evaluasi Model** — Metrik MAE, RMSE, R² vs baseline naive + scatter plot aktual vs prediksi
- **🔍 Data Mentah** — Tabel data lengkap + tombol download CSV

### Konsep yang Dipelajari
- Time series sebagai supervised learning problem
- Lag features sebagai transformasi data
- Train/test split time-aware (tidak diacak)
- Forecast iteratif (prediksi t+1 → input untuk t+2)
- Evaluasi model: MAE, RMSE, R²
- Perbandingan model vs baseline naive

---

## 👥 App 2: Customer Segmentation

**File:** `app_segmentasi.py` | **Port:** `8502`

Demo segmentasi pelanggan menggunakan **Unsupervised Learning (KMeans Clustering)**.

### Sumber Data (pilih satu)
| Opsi | Deskripsi |
|------|-----------|
| 👥 Data Demo | 200 pelanggan sintetis (3 cluster: Pasif, Potensial, Premium) |
| 📁 Upload CSV | Upload CSV dengan minimal 2 kolom numerik |

### Data Demo — Profil Cluster Bawaan
| Cluster | Jumlah | Usia | Pengeluaran/Bulan | Frekuensi Transaksi |
|---------|--------|------|-------------------|---------------------|
| 😴 Pasif | 60 org | 20–30 thn | Rp 200–400rb | 1–3x/bulan |
| 🌱 Potensial | 80 org | 30–50 thn | Rp 500–900rb | 4–7x/bulan |
| 💎 Premium | 60 org | 35–60 thn | Rp 1.000–2.000rb | 8–15x/bulan |

### Format CSV Upload (App 2)
```
usia,pengeluaran,frekuensi,kota
25,350000,2,Jakarta
42,750000,5,Surabaya
55,1500000,12,Bandung
...
```
- Minimal 2 kolom numerik
- Kolom non-numerik diabaikan otomatis
- Setelah upload, pilih kolom mana yang dipakai untuk clustering

### Parameter (Sidebar)
| Parameter | Range | Default | Keterangan |
|-----------|-------|---------|------------|
| Jumlah Cluster K | 2–6 | 3 | Jumlah segmen yang dibentuk |
| Tampilkan Interpretasi | checkbox | OFF | Aktifkan label + narasi bisnis per cluster |

### Tabs
- **🗺️ Visualisasi Cluster** — Scatter plot PCA 2D dengan centroid bintang ★
- **📊 Profil Cluster** — Tabel rata-rata fitur + grouped bar chart + narasi bisnis (jika interpretasi ON)
- **📉 Elbow Method** — Grafik inertia K=1–10 untuk memilih K optimal

### Konsep yang Dipelajari
- Unsupervised learning vs supervised learning
- KMeans clustering — cara kerja dan inisialisasi
- Feature scaling (StandardScaler) — mengapa penting sebelum clustering
- PCA — reduksi dimensi untuk visualisasi
- Elbow method — mencari jumlah cluster optimal
- Interpretasi bisnis dari hasil clustering

---

## 🧠 App 3: CNN Image Classification

**File:** `app_cnn.py` | **Port:** `8503` | **Sesi:** 4 — Deep Learning

Demo klasifikasi gambar menggunakan **Convolutional Neural Network (CNN)** dengan PyTorch pada dataset CIFAR-10.

### Dataset
**CIFAR-10** — 60.000 gambar berwarna ukuran **32×32 piksel**, 10 kelas:

| Kelas | Emoji | Kelas | Emoji |
|-------|-------|-------|-------|
| Pesawat | ✈️ | Rusa | 🦌 |
| Mobil | 🚗 | Anjing | 🐶 |
| Burung | 🐦 | Katak | 🐸 |
| Kucing | 🐱 | Kuda | 🐴 |
| — | — | Kapal | 🚢 |
| — | — | Truk | 🚛 |

### Arsitektur Model — SimpleCNN
```
Input (3×32×32)
    ↓ Blok 1: Conv2d(3→32) → BN → ReLU → Conv2d(32→32) → BN → ReLU → MaxPool2d → Dropout2d
    ↓ Blok 2: Conv2d(32→64) → BN → ReLU → Conv2d(64→64) → BN → ReLU → MaxPool2d → Dropout2d
    ↓ Flatten (64×8×8 = 4.096)
    ↓ Linear(4096→256) → ReLU → Dropout(0.4)
    ↓ Linear(256→10) → Softmax
Output: 10 probabilitas kelas
```

### Parameter Training (Sidebar)
| Parameter | Pilihan | Default | Keterangan |
|-----------|---------|---------|------------|
| Data Latih | 500 / 1.000 / 2.000 / 5.000 | 1.000 | Subset dari 50.000 data train CIFAR-10 |
| Data Uji | 200 / 500 / 1.000 | 500 | Subset dari 10.000 data test CIFAR-10 |
| Model | CNN / MLP | CNN | CNN = konvolusi; MLP = fully-connected saja |
| Epoch | 1–20 | 5 | Berapa kali model melihat seluruh data latih |
| Batch Size | 32 / 64 / 128 | 64 | Jumlah sampel per update gradien |
| Learning Rate | 0.0001–0.1 | 0.001 | Kecepatan update bobot |
| Optimizer | Adam / SGD | Adam | Adam = adaptif; SGD = klasik dengan momentum |

### Cara Prediksi Gambar (Tab 2)
Setelah model selesai dilatih, buka tab **🔍 Prediksi Gambar**. Tersedia **dua pilihan input**:

**Opsi 1 — 🎲 Gunakan Sampel dari Dataset CIFAR-10**
- Tekan tombol **🎲 Acak Gambar** untuk ambil gambar acak
- Atau filter berdasarkan kelas tertentu (✈️ Pesawat, 🚗 Mobil, dll.)
- Atau geser slider untuk navigasi manual per indeks
- Gambar langsung ditampilkan beserta kelas aslinya
- Hasil prediksi + confidence muncul otomatis

**Opsi 2 — 📁 Upload Gambar Sendiri**
- Upload file JPG / PNG dari perangkat Anda
- Model otomatis meresize ke 32×32 piksel
- Tampilan side-by-side: gambar asli vs hasil resize
- Prediksi dijalankan otomatis setelah upload

### Tabs
- **📈 Hasil Training** — Grafik akurasi & loss per epoch (live update saat training), deteksi overfitting otomatis
- **🔍 Prediksi Gambar** — Prediksi dengan 2 pilihan input (sampel CIFAR-10 atau upload sendiri)
- **🏗️ Arsitektur CNN** — Tabel layer-by-layer, diagram dimensi data, penjelasan konsep kunci
- **⚖️ CNN vs ML Klasik** — Benchmark CNN vs SVM (RBF) vs Random Forest pada piksel mentah

### Konsep yang Dipelajari
- Konvolusi (Conv2d) — deteksi pola spasial lokal
- Batch Normalization — stabilisasi training
- Max Pooling — reduksi dimensi + translasi invariance
- Dropout — regularisasi untuk mencegah overfitting
- Feature learning vs feature engineering manual
- Overfitting detection (gap train vs val accuracy)
- Perbandingan CNN vs ML klasik pada data gambar
- Distribusi shift — kenapa akurasi pada gambar luar dataset bisa turun

---

## 🛠️ Dependencies

```
streamlit
pyngrok
plotly
scikit-learn
pandas
numpy
yfinance
torch
torchvision
Pillow
```

Semua diinstall otomatis via Cell 1 notebook.

---

## ⚠️ Troubleshooting

### Error: "tunnel limit reached" / "too many connections"
```python
# Jalankan Cell 9 (kill cell) untuk stop semua tunnel, lalu jalankan ulang runner cell
ngrok.kill()
```

### Error: "authtoken is not set" atau "authentication failed"
- Pastikan Cell 2 sudah dijalankan dengan token yang valid
- Cek token di [dashboard.ngrok.com](https://dashboard.ngrok.com/get-started/your-authtoken)

### Error: ticker saham tidak ditemukan
- Pastikan kode ticker benar (contoh: `BBCA.JK` bukan `BBCA`)
- Untuk saham Indonesia di yfinance, tambahkan `.JK` di belakang
- Contoh valid: `BBCA.JK`, `TLKM.JK`, `GOTO.JK`, `AAPL`, `TSLA`, `GOOGL`

### App tidak muncul setelah klik URL
- Ngrok menampilkan halaman peringatan → klik **"Visit Site"**
- Jika loading lama, tunggu ~10 detik lalu refresh

### Runtime Colab timeout / restart
- Semua cell harus dijalankan ulang dari awal (Cell 1 → 2 → 3 → 4 → 5 → ...)
- File `.py` hilang saat runtime restart, cell `%%writefile` harus dijalankan ulang

### Data CSV tidak terbaca
- Pastikan file encoding UTF-8
- Cek tidak ada karakter spesial di nama kolom
- Untuk App 1: pastikan format tanggal `YYYY-MM` atau `YYYY-MM-DD`
- Untuk App 2: pastikan ada minimal 2 kolom dengan data angka

### App 3: Download CIFAR-10 lambat
- CIFAR-10 ~170MB, didownload sekali lalu di-cache
- Jika runtime restart, download ulang otomatis saat app pertama kali dibuka

---

## 📐 Arsitektur Teknis

```
Google Colab Runtime
│
├── Cell 3 (%%writefile) ──→ app_timeseries.py
├── Cell 4 (%%writefile) ──→ app_segmentasi.py
├── Cell 5 (%%writefile) ──→ app_cnn.py
│
├── Cell 6 ──→ subprocess: streamlit run app_timeseries.py --port 8501
│              └── ngrok tunnel: public URL → localhost:8501
│
├── Cell 7 ──→ subprocess: streamlit run app_segmentasi.py --port 8502
│              └── ngrok tunnel: public URL → localhost:8502
│
└── Cell 8 ──→ subprocess: streamlit run app_cnn.py --port 8503
               └── ngrok tunnel: public URL → localhost:8503
```

### Alur Data — App 1 (Time Series)
```
Input Data
    ↓
Buat Lag Features (lag_1 ... lag_n)
    ↓
Train/Test Split (80% / 20%, time-aware)
    ↓
Training Model (Linear / Ridge / Decision Tree)
    ↓
Prediksi pada Test Set → Evaluasi (MAE, RMSE, R²)
    ↓
Forecast Iteratif → n periode ke depan
```

### Alur Data — App 2 (Segmentasi)
```
Input Data
    ↓
StandardScaler (normalisasi fitur)
    ↓
KMeans Clustering (n_clusters=K, n_init=10, random_state=42)
    ↓
Assign Label Cluster (ranking by proxy column)
    ↓
PCA 2 Komponen (untuk visualisasi saja)
    ↓
Visualisasi + Profil + Elbow Method
```

### Alur Data — App 3 (CNN)
```
Input Gambar (32×32 RGB)
    ↓
Normalisasi (mean=[0.4914,0.4822,0.4465], std=[0.2023,0.1994,0.2010])
    ↓
Blok Konvolusi 1 (Conv→BN→ReLU×2 → MaxPool → Dropout)
    ↓
Blok Konvolusi 2 (Conv→BN→ReLU×2 → MaxPool → Dropout)
    ↓
Flatten → Fully Connected (4096→256→10)
    ↓
Softmax → 10 Probabilitas Kelas
```

---

## 📝 Catatan untuk Instruktur

- Semua app langsung jalan tanpa input apapun (data demo / dataset sudah tersedia sebagai default)
- Parameter sidebar bisa diubah real-time, semua chart dan metrik update otomatis
- **App 1:** gunakan slider lag untuk demonstrasi underfitting vs overfitting
- **App 1:** gunakan data saham untuk memperlihatkan keterbatasan model linear pada data noisy
- **App 2:** gunakan slider K untuk demonstrasi efek jumlah cluster pada Elbow Method
- **App 2:** aktifkan "Tampilkan Interpretasi Cluster" untuk sesi diskusi bisnis
- **App 3:** bandingkan CNN vs MLP untuk menjelaskan keunggulan konvolusi pada data spasial
- **App 3:** gunakan Tab ⚖️ untuk benchmark live CNN vs SVM vs Random Forest
- **App 3:** demonstrasikan distribusi shift dengan upload foto dari luar dataset CIFAR-10
- Ketiga app bisa berjalan bersamaan (port berbeda: 8501, 8502, 8503)

---

*Dibuat untuk kebutuhan kelas Machine Learning — RubyThalib*
