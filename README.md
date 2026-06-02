# 🤖 ML Demo Apps — Machine Learning Interactive Demo

Dua aplikasi Streamlit interaktif untuk kelas Machine Learning, dirancang untuk dijalankan di **Google Colab** dengan akses publik via **ngrok tunneling**.

---

## 📦 Isi Proyek

```
ml-demo-apps/
└── ML_Demo_Apps.ipynb    ← Satu notebook berisi semua (setup + 2 app + runner)
```

Saat notebook dijalankan, dua file app akan dibuat otomatis di Colab:
```
app_timeseries.py         ← App 1: Time Series Forecasting
app_segmentasi.py         ← App 2: Customer Segmentation
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
| **Cell 1** | ▶ Jalankan | Install semua dependencies (~1-2 menit) |
| **Cell 2** | Edit token lalu ▶ | Ganti `YOUR_NGROK_AUTHTOKEN_HERE` dengan token Anda |
| **Cell 3** | ▶ Jalankan | Membuat file `app_timeseries.py` |
| **Cell 4** | ▶ Jalankan | Membuat file `app_segmentasi.py` |
| **Cell 5** | ▶ Jalankan | Menjalankan App 1 → klik URL yang muncul |
| **Cell 6** | ▶ Jalankan | Menjalankan App 2 → klik URL yang muncul |
| **Cell 7** | *(Opsional)* | Menghentikan semua tunnel ngrok |

**4. Buka Aplikasi**

Setelah Cell 5 atau 6 dijalankan, output akan tampil seperti ini:
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

## 🛠️ Dependencies

```
streamlit
pyngrok
plotly
scikit-learn
pandas
numpy
yfinance
```

Semua diinstall otomatis via Cell 1 notebook.

---

## ⚠️ Troubleshooting

### Error: "tunnel limit reached" / "too many connections"
```python
# Jalankan Cell 7 untuk kill semua tunnel, lalu jalankan ulang Cell 5/6
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
- Semua cell harus dijalankan ulang dari awal (Cell 1 → 2 → 3 → 4 → 5/6)
- File `.py` hilang saat runtime restart, Cell 3 & 4 harus dijalankan lagi

### Data CSV tidak terbaca
- Pastikan file encoding UTF-8
- Cek tidak ada karakter spesial di nama kolom
- Untuk App 1: pastikan format tanggal `YYYY-MM` atau `YYYY-MM-DD`
- Untuk App 2: pastikan ada minimal 2 kolom dengan data angka

---

## 📐 Arsitektur Teknis

```
Google Colab Runtime
│
├── Cell 3 (%%writefile) ──→ app_timeseries.py
├── Cell 4 (%%writefile) ──→ app_segmentasi.py
│
├── Cell 5 ──→ subprocess: streamlit run app_timeseries.py --port 8501
│              └── ngrok tunnel: public URL → localhost:8501
│
└── Cell 6 ──→ subprocess: streamlit run app_segmentasi.py --port 8502
               └── ngrok tunnel: public URL → localhost:8502
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

---

## 📝 Catatan untuk Instruktur

- Semua app langsung jalan tanpa input apapun (data demo sudah tersedia sebagai default state)
- Parameter sidebar bisa diubah real-time, semua chart dan metrik update otomatis
- **App 1:** gunakan slider lag untuk demonstrasi underfitting vs overfitting
- **App 1:** gunakan data saham untuk memperlihatkan keterbatasan model linear pada data noisy
- **App 2:** gunakan slider K untuk demonstrasi efek jumlah cluster pada Elbow Method
- **App 2:** aktifkan "Tampilkan Interpretasi Cluster" untuk sesi diskusi bisnis
- Kedua app bisa berjalan bersamaan (port berbeda: 8501 dan 8502)

---

*Dibuat untuk kebutuhan kelas Machine Learning — RubyThalib*
