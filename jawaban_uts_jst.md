# JAWABAN UTS JARINGAN SYARAF TIRUAN
**Universitas Indraprasta PGRI (UNINDRA)**  
**Fakultas Teknik dan Ilmu Komputer**  
**Mata Kuliah: Jaringan Syaraf Tiruan (+)**  
**Tahun Akademik 2025/2026**

---

## SOAL 1 — Arsitektur Perceptron Single Layer dan McCulloch-Pitts (McP)
> *Buatlah arsitektur jaringan Perceptron Single Layer dan McP jika diketahui jumlah input 5 neuron dengan luaran jaringan sebanyak 2. Besaran bobot dan parameter lainnya ditentukan oleh Anda dengan asumsi sebagai bobot akhir pelatihan suatu model!*

### A. Asumsi Parameter

| Parameter | Nilai |
|-----------|-------|
| Jumlah Input (n) | 5 neuron (x₁, x₂, x₃, x₄, x₅) |
| Jumlah Output (m) | 2 neuron (y₁, y₂) |
| Bias | b = 1 |
| Fungsi Aktivasi | Step Function (threshold θ = 0.5) |

### B. Bobot Akhir Pelatihan (Asumsi)

**Bobot untuk Output y₁:**

| Bobot | Nilai |
|-------|-------|
| w₁₁ (x₁ → y₁) | 0.6 |
| w₂₁ (x₂ → y₁) | 0.4 |
| w₃₁ (x₃ → y₁) | -0.3 |
| w₄₁ (x₄ → y₁) | 0.7 |
| w₅₁ (x₅ → y₁) | 0.5 |
| b₁ (bias → y₁) | -0.5 |

**Bobot untuk Output y₂:**

| Bobot | Nilai |
|-------|-------|
| w₁₂ (x₁ → y₂) | -0.4 |
| w₂₂ (x₂ → y₂) | 0.8 |
| w₃₂ (x₃ → y₂) | 0.6 |
| w₄₂ (x₄ → y₂) | -0.2 |
| w₅₂ (x₅ → y₂) | 0.3 |
| b₂ (bias → y₂) | -0.3 |

### C. Arsitektur Perceptron Single Layer

```
        x₁ ──w₁₁──┐
        x₂ ──w₂₁──┤         ┌──── y₁ (Output 1)
        x₃ ──w₃₁──┼──[∑]──[f(net)]
        x₄ ──w₄₁──┤
        x₅ ──w₅₁──┘
        b  ──b₁───┘

        x₁ ──w₁₂──┐
        x₂ ──w₂₂──┤         ┌──── y₂ (Output 2)
        x₃ ──w₃₂──┼──[∑]──[f(net)]
        x₄ ──w₄₂──┤
        x₅ ──w₅₂──┘
        b  ──b₂───┘
```

**Keterangan:**
- Layer Input  : 5 neuron (x₁ s.d. x₅) + 1 bias
- Layer Output : 2 neuron (y₁ dan y₂)
- Tidak ada hidden layer → disebut **Single Layer**
- Setiap input terhubung ke **setiap** output (fully connected)
- Total bobot : 5×2 + 2 (bias) = **12 bobot**

### D. Fungsi Aktivasi (Step Function)

```
         net_j = Σ(wᵢⱼ · xᵢ) + bⱼ

              ⎧  1,  jika net_j ≥ θ (θ = 0.5)
    f(net) =  ⎨
              ⎩  0,  jika net_j < θ
```

### E. Contoh Perhitungan (Verifikasi Bobot)

Misal input: **x = [1, 0, 1, 1, 0]**

**Untuk y₁:**
```
net₁ = (0.6×1) + (0.4×0) + (-0.3×1) + (0.7×1) + (0.5×0) + (-0.5×1)
     = 0.6 + 0 - 0.3 + 0.7 + 0 - 0.5
     = 0.5
y₁   = f(0.5) = 1  (karena net₁ ≥ 0.5)
```

**Untuk y₂:**
```
net₂ = (-0.4×1) + (0.8×0) + (0.6×1) + (-0.2×1) + (0.3×0) + (-0.3×1)
     = -0.4 + 0 + 0.6 - 0.2 + 0 - 0.3
     = -0.3
y₂   = f(-0.3) = 0  (karena net₂ < 0.5)
```

**Output: y = [1, 0]**

### F. Arsitektur McCulloch-Pitts (McP)

Model McP menggunakan bobot **biner** dan **threshold tetap** tanpa proses pembelajaran:

```
        x₁ ──(+1)──┐
        x₂ ──(+1)──┤
        x₃ ──(-1)──┼──[∑]──[θ=3]──→ y₁
        x₄ ──(+1)──┤
        x₅ ──(+1)──┘

        x₁ ──(-1)──┐
        x₂ ──(+1)──┤
        x₃ ──(+1)──┼──[∑]──[θ=2]──→ y₂
        x₄ ──(-1)──┤
        x₅ ──(+1)──┘
```

**Perbedaan Perceptron vs McP:**

| Aspek | Perceptron | McCulloch-Pitts (McP) |
|-------|-----------|----------------------|
| Bobot | Real (desimal), bisa dilatih | Biner (+1/-1), tetap |
| Bias | Ada, bisa dilatih | Tidak ada |
| Pembelajaran | Ada (update bobot) | Tidak ada |
| Input | Real / biner | Biner saja |
| Fungsi aktivasi | Step / Sigmoid | Step (threshold) |

---

## SOAL 2 — Analisis Kasus Spam Email
> *Perusahaan email mengembangkan model Neural Network untuk klasifikasi spam/non-spam berdasarkan data berlabel.*

### A. Pendekatan: Supervised Learning atau Unsupervised Learning?

**Jawaban: SUPERVISED LEARNING**

**Alasan:**
1. Data email yang digunakan telah **diberi label** secara eksplisit, yaitu **"spam"** dan **"bukan spam"**.
2. Model dilatih menggunakan **pasangan input-output** (isi email → label kategori).
3. Tujuannya adalah **memprediksi label** untuk data baru (email masuk), yang merupakan ciri khas supervised learning.
4. Proses pelatihan menggunakan **fungsi loss** yang membandingkan prediksi model dengan label sebenarnya, lalu melakukan koreksi bobot.

> Unsupervised learning **tidak digunakan** karena data **sudah berlabel**. Unsupervised learning dipakai jika data tidak memiliki label (misalnya clustering email tanpa kategori tertentu).

### B. Contoh Dataset

| No | Fitur Pesan | Label |
|----|-------------|-------|
| 1 | "Selamat! Anda menang hadiah 1 juta, klik link ini" | Spam |
| 2 | "Laporan keuangan Q1 terlampir, mohon ditinjau" | Bukan Spam |
| 3 | "GRATIS iPhone, daftar sekarang!" | Spam |
| 4 | "Rapat tim besok jam 09.00 pagi" | Bukan Spam |
| 5 | "Verifikasi akun Anda segera atau akun ditutup!" | Spam |
| 6 | "Terima kasih atas pembelian Anda, nomor order #12345" | Bukan Spam |

**Fitur yang diekstrak dari email:**
- Frekuensi kata tertentu (e.g., "gratis", "menang", "klik")
- Keberadaan tautan/URL mencurigakan (0 atau 1)
- Pola waktu pengiriman
- Panjang pesan
- Penggunaan huruf kapital berlebihan

### C. Apakah Bisa Diselesaikan dengan Perceptron?

**Jawaban: TIDAK OPTIMAL menggunakan Perceptron sederhana**

**Alasan:**
1. **Perceptron hanya bisa menyelesaikan masalah yang *linearly separable*** — artinya data harus bisa dipisahkan dengan satu garis lurus di ruang fitur.
2. Data email di dunia nyata **sangat kompleks dan tidak linier** — pola spam tidak bisa dipisahkan secara linear dari non-spam.
3. Perceptron hanya memiliki **satu layer** tanpa kemampuan menangkap representasi fitur yang kompleks.
4. Fitur email berdimensi tinggi (ribuan kata) dengan interaksi non-linear antar fitur.

### D. Rekomendasi Algoritma yang Lebih Cocok

| Algoritma | Keunggulan untuk Kasus Ini |
|-----------|---------------------------|
| **Multi-Layer Perceptron (MLP) / Deep Neural Network** | Mampu menangkap pola non-linear kompleks dalam teks email |
| **Recurrent Neural Network (RNN) / LSTM** | Mempertimbangkan urutan kata dalam kalimat email |
| **Naive Bayes** | Sangat efektif dan efisien untuk klasifikasi teks, probabilistik |
| **Support Vector Machine (SVM)** | Efektif untuk data berdimensi tinggi seperti bag-of-words |
| **Random Forest** | Robust terhadap noise, menangani banyak fitur dengan baik |

**Rekomendasi Utama: Multi-Layer Perceptron (MLP)**
- Memiliki hidden layer sehingga mampu belajar representasi fitur non-linear
- Cocok dengan data berlabel (supervised)
- Dapat dikombinasikan dengan teknik NLP (TF-IDF, Word Embedding)

---

## SOAL 3 — Pelatihan Adaline
> *Dataset A dilatih dengan Adaline: θ = 1, α = 0.8, toleransi = 0.05, max epoch = 1*

### A. Tabel Dataset & Konversi Bipolar

**Data Asli (Binary):**

| No | X₁ | X₂ | X₃ | Target |
|----|----|----|-----|--------|
| 1  | 1  | 0  | 1   | 1      |
| 2  | 1  | 0  | 0   | 1      |
| 3  | 1  | 1  | 1   | 1      |
| 4  | 0  | 1  | 0   | 1      |
| 5  | 0  | 0  | 1   | 1      |
| 6  | 0  | 0  | 0   | 0      |

**Konversi ke Bipolar** (0 → -1, 1 → +1):

| No | X₁ | X₂ | X₃ | Target (t) |
|----|----|----|-----|-----------|
| 1  | +1 | -1 | +1  | +1        |
| 2  | +1 | -1 | -1  | +1        |
| 3  | +1 | +1 | +1  | +1        |
| 4  | -1 | +1 | -1  | +1        |
| 5  | -1 | -1 | +1  | +1        |
| 6  | -1 | -1 | -1  | -1        |

### B. Fungsi Aktivasi Adaline & Inisialisasi

**Fungsi Aktivasi Adaline:**
```
Adaline menggunakan fungsi aktivasi LINEAR pada saat pelatihan:
    y_in = b + Σ(xᵢ · wᵢ)   ← output net (sebelum threshold)

Untuk OUTPUT AKHIR (prediksi klasifikasi) digunakan Bipolar Step:
         ⎧ +1,  jika y_in ≥ θ (θ = 1)
f(y_in)= ⎨
         ⎩ -1,  jika y_in < θ

Update bobot menggunakan DELTA RULE (Least Mean Square - LMS):
    Δwᵢ = α · (t - y_in) · xᵢ
    wᵢ(baru) = wᵢ(lama) + Δwᵢ
    Δb  = α · (t - y_in)
    b(baru) = b(lama) + Δb
```

**Inisialisasi Awal:**
```
w₁ = 0,  w₂ = 0,  w₃ = 0,  b = 0
α  = 0.8,  θ = 1,  toleransi = 0.05
```

### C. Pelatihan Epoch 1

---

**Data ke-1: x = [+1, -1, +1], t = +1**

```
y_in = b + w₁x₁ + w₂x₂ + w₃x₃
     = 0 + (0)(1) + (0)(-1) + (0)(1)
     = 0

Error = t - y_in = 1 - 0 = 1

Update:
  Δw₁ = α · error · x₁ = 0.8 × 1 × (+1) =  0.8  → w₁ = 0 + 0.8  =  0.8
  Δw₂ = α · error · x₂ = 0.8 × 1 × (-1) = -0.8  → w₂ = 0 + (-0.8) = -0.8
  Δw₃ = α · error · x₃ = 0.8 × 1 × (+1) =  0.8  → w₃ = 0 + 0.8  =  0.8
  Δb  = α · error      = 0.8 × 1         =  0.8  → b  = 0 + 0.8  =  0.8

Bobot baru: w₁=0.8, w₂=-0.8, w₃=0.8, b=0.8
SSE (data 1) = (1)² = 1
```

---

**Data ke-2: x = [+1, -1, -1], t = +1**

```
y_in = 0.8 + (0.8)(1) + (-0.8)(-1) + (0.8)(-1)
     = 0.8 + 0.8 + 0.8 - 0.8
     = 1.6

Error = t - y_in = 1 - 1.6 = -0.6

Update:
  Δw₁ = 0.8 × (-0.6) × (+1) = -0.48 → w₁ = 0.8 - 0.48  =  0.32
  Δw₂ = 0.8 × (-0.6) × (-1) =  0.48 → w₂ = -0.8 + 0.48 = -0.32
  Δw₃ = 0.8 × (-0.6) × (-1) =  0.48 → w₃ = 0.8 + 0.48  =  1.28
  Δb  = 0.8 × (-0.6)         = -0.48 → b  = 0.8 - 0.48  =  0.32

Bobot baru: w₁=0.32, w₂=-0.32, w₃=1.28, b=0.32
SSE (data 2) = (-0.6)² = 0.36
```

---

**Data ke-3: x = [+1, +1, +1], t = +1**

```
y_in = 0.32 + (0.32)(1) + (-0.32)(1) + (1.28)(1)
     = 0.32 + 0.32 - 0.32 + 1.28
     = 1.60

Error = t - y_in = 1 - 1.60 = -0.60

Update:
  Δw₁ = 0.8 × (-0.60) × (+1) = -0.48 → w₁ = 0.32 - 0.48  = -0.16
  Δw₂ = 0.8 × (-0.60) × (+1) = -0.48 → w₂ = -0.32 - 0.48 = -0.80
  Δw₃ = 0.8 × (-0.60) × (+1) = -0.48 → w₃ = 1.28 - 0.48  =  0.80
  Δb  = 0.8 × (-0.60)         = -0.48 → b  = 0.32 - 0.48  = -0.16

Bobot baru: w₁=-0.16, w₂=-0.80, w₃=0.80, b=-0.16
SSE (data 3) = (-0.60)² = 0.36
```

---

**Data ke-4: x = [-1, +1, -1], t = +1**

```
y_in = -0.16 + (-0.16)(-1) + (-0.80)(1) + (0.80)(-1)
     = -0.16 + 0.16 - 0.80 - 0.80
     = -1.60

Error = t - y_in = 1 - (-1.60) = 2.60

Update:
  Δw₁ = 0.8 × 2.60 × (-1) = -2.08 → w₁ = -0.16 - 2.08 = -2.24
  Δw₂ = 0.8 × 2.60 × (+1) =  2.08 → w₂ = -0.80 + 2.08 =  1.28
  Δw₃ = 0.8 × 2.60 × (-1) = -2.08 → w₃ = 0.80 - 2.08  = -1.28
  Δb  = 0.8 × 2.60         =  2.08 → b  = -0.16 + 2.08 =  1.92

Bobot baru: w₁=-2.24, w₂=1.28, w₃=-1.28, b=1.92
SSE (data 4) = (2.60)² = 6.76
```

---

**Data ke-5: x = [-1, -1, +1], t = +1**

```
y_in = 1.92 + (-2.24)(-1) + (1.28)(-1) + (-1.28)(1)
     = 1.92 + 2.24 - 1.28 - 1.28
     = 1.60

Error = t - y_in = 1 - 1.60 = -0.60

Update:
  Δw₁ = 0.8 × (-0.60) × (-1) =  0.48 → w₁ = -2.24 + 0.48 = -1.76
  Δw₂ = 0.8 × (-0.60) × (-1) =  0.48 → w₂ =  1.28 + 0.48 =  1.76
  Δw₃ = 0.8 × (-0.60) × (+1) = -0.48 → w₃ = -1.28 - 0.48 = -1.76
  Δb  = 0.8 × (-0.60)         = -0.48 → b  =  1.92 - 0.48 =  1.44

Bobot baru: w₁=-1.76, w₂=1.76, w₃=-1.76, b=1.44
SSE (data 5) = (-0.60)² = 0.36
```

---

**Data ke-6: x = [-1, -1, -1], t = -1**

```
y_in = 1.44 + (-1.76)(-1) + (1.76)(-1) + (-1.76)(-1)
     = 1.44 + 1.76 - 1.76 + 1.76
     = 3.20

Error = t - y_in = -1 - 3.20 = -4.20

Update:
  Δw₁ = 0.8 × (-4.20) × (-1) =  3.36 → w₁ = -1.76 + 3.36 =  1.60
  Δw₂ = 0.8 × (-4.20) × (-1) =  3.36 → w₂ =  1.76 + 3.36 =  5.12
  Δw₃ = 0.8 × (-4.20) × (-1) =  3.36 → w₃ = -1.76 + 3.36 =  1.60
  Δb  = 0.8 × (-4.20)         = -3.36 → b  =  1.44 - 3.36 = -1.92

Bobot baru: w₁=1.60, w₂=5.12, w₃=1.60, b=-1.92
SSE (data 6) = (-4.20)² = 17.64
```

---

### Tabel Rekapitulasi Pelatihan Epoch 1

| Data | x₁ | x₂ | x₃ | t  | y_in  | Error | w₁(baru) | w₂(baru) | w₃(baru) | b(baru) | SSE   |
|------|----|----|-----|----|----- -|-------|----------|----------|----------|---------|-------|
| 0 (init) | - | - | -  | -  | -     | -     | 0        | 0        | 0        | 0       | -     |
| 1    | +1 | -1 | +1  | +1 | 0.00  | 1.00  | 0.80     | -0.80    | 0.80     | 0.80    | 1.00  |
| 2    | +1 | -1 | -1  | +1 | 1.60  | -0.60 | 0.32     | -0.32    | 1.28     | 0.32    | 0.36  |
| 3    | +1 | +1 | +1  | +1 | 1.60  | -0.60 | -0.16    | -0.80    | 0.80     | -0.16   | 0.36  |
| 4    | -1 | +1 | -1  | +1 | -1.60 | 2.60  | -2.24    | 1.28     | -1.28    | 1.92    | 6.76  |
| 5    | -1 | -1 | +1  | +1 | 1.60  | -0.60 | -1.76    | 1.76     | -1.76    | 1.44    | 0.36  |
| 6    | -1 | -1 | -1  | -1 | 3.20  | -4.20 | 1.60     | 5.12     | 1.60     | -1.92   | 17.64 |

**Total SSE Epoch 1:**
```
SSE_total = 1.00 + 0.36 + 0.36 + 6.76 + 0.36 + 17.64 = 26.48
MSE (Mean Square Error) = SSE_total / 6 = 26.48 / 6 ≈ 4.41
```

### C. Apakah Model Memahami Pola di Epoch 1?

**Jawaban: TIDAK**

**Alasan:**
- Total SSE pada epoch 1 = **26.48**, jauh di atas toleransi 0.05
- MSE ≈ 4.41, sangat jauh dari nilai konvergensi
- Bobot berubah sangat drastis (terutama pada data ke-4 dan ke-6), menunjukkan model **belum stabil**
- Terdapat error yang sangat besar: data ke-6 menghasilkan error = -4.20, yang menunjukkan model belum bisa membedakan pola kelas -1

### D. Apakah Perlu Melanjutkan Epoch ke-2?

**Jawaban: YA, perlu melanjutkan pelatihan**

**Alasan:**
```
Kondisi berhenti Adaline:
  MSE ≤ toleransi  →  4.41 ≤ 0.05  →  TIDAK TERPENUHI

Maka pelatihan HARUS dilanjutkan ke epoch berikutnya
(hingga MSE ≤ 0.05 atau mencapai batas epoch maksimum)
```

### E. Arsitektur Jaringan Adaline (Hasil Akhir Epoch 1)

```
         x₁ (+1/-1)  ──── w₁ = 1.60 ────┐
                                          │
         x₂ (+1/-1)  ──── w₂ = 5.12 ────┤
                                          ├──[∑ y_in]──[f: Bipolar Step θ=1]──→ y (+1/-1)
         x₃ (+1/-1)  ──── w₃ = 1.60 ────┤
                                          │
         Bias (1)     ────  b = -1.92 ───┘

    y_in = -1.92 + 1.60·x₁ + 5.12·x₂ + 1.60·x₃

              ⎧ +1,  jika y_in ≥ 1
    f(y_in) = ⎨
              ⎩ -1,  jika y_in < 1

    Update rule (LMS):
      wᵢ(baru) = wᵢ(lama) + α·(t - y_in)·xᵢ
      b(baru)  = b(lama)  + α·(t - y_in)
```

**Keterangan Arsitektur:**
- **Input Layer**: 3 neuron (x₁, x₂, x₃) + 1 bias
- **Output Layer**: 1 neuron dengan fungsi aktivasi Bipolar Step
- **Tidak ada hidden layer** (arsitektur single layer)
- **Bobot akhir epoch 1**: w₁=1.60, w₂=5.12, w₃=1.60, b=-1.92
- Model belum konvergen → butuh pelatihan lanjutan

---

*Dikerjakan sesuai materi Jaringan Syaraf Tiruan — Perceptron, McP, dan Adaline*
*Universitas Indraprasta PGRI (UNINDRA) — T.A. 2025/2026*
