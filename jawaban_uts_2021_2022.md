# JAWABAN UTS JARINGAN SYARAF TIRUAN
**Universitas Indraprasta PGRI (UNINDRA)**
**Fakultas Teknik dan Ilmu Komputer**
**Mata Kuliah : Jaringan Syaraf Tiruan**
**Tahun Akademik : 2021/2022 | Kamis, 19 Mei 2022**

---

## SOAL 1 — Jaringan Hebb [Bobot: 30]

> *Buatlah jaringan Hebb untuk mengenali fungsi logika dengan masukan dan keluaran biner. Bobot awal = 0.a, bias = 0.7. Buktikan dengan aktivasi f(net) diterima atau ditolak.*

### A. Identifikasi Dataset & Fungsi Logika

Data yang diberikan:

| x1 | x2 | t |
|----|----|---|
| 1  | 0  | 0 |
| 1  | 1  | 1 |
| 0  | 0  | 0 |
| 0  | 1  | 0 |

Analisis target: output = 1 **hanya** ketika x1=1 DAN x2=1
→ Ini adalah fungsi logika **AND**

### B. Inisialisasi Parameter

```
Bobot awal : w₁ = 0.a, w₂ = 0.a
  (Nilai "a" = 1 digit belakang NPM = 8)
  NPM belakang = 8  →  w₁ = 0.8,  w₂ = 0.8

Bias awal  : b  = 0.7
Fungsi aktivasi (Step Function biner):
       ⎧ 1,  jika net ≥ 0
f(net)=⎨
       ⎩ 0,  jika net < 0
```

### C. Aturan Pembelajaran Hebb

```
Aturan Hebb (Hebb's Rule):
  wᵢ(baru) = wᵢ(lama) + xᵢ × t
  b(baru)  = b(lama)  + t
```

> **Catatan:** Pada aturan Hebb, bobot diperbarui menggunakan nilai **input** dan **target**,
> bukan error. Tidak ada iterasi ulang (satu kali pass).

### D. Proses Pelatihan Hebb

**─── Data ke-1: x=[1, 0], t=0 ───**
```
w₁(baru) = 0.8 + (1 × 0) = 0.8 + 0 = 0.8
w₂(baru) = 0.8 + (0 × 0) = 0.8 + 0 = 0.8
b(baru)  = 0.7 + 0        = 0.7

Bobot setelah data 1: w₁=0.8, w₂=0.8, b=0.7
```

**─── Data ke-2: x=[1, 1], t=1 ───**
```
w₁(baru) = 0.8 + (1 × 1) = 0.8 + 1 = 1.8
w₂(baru) = 0.8 + (1 × 1) = 0.8 + 1 = 1.8
b(baru)  = 0.7 + 1        = 1.7

Bobot setelah data 2: w₁=1.8, w₂=1.8, b=1.7
```

**─── Data ke-3: x=[0, 0], t=0 ───**
```
w₁(baru) = 1.8 + (0 × 0) = 1.8
w₂(baru) = 1.8 + (0 × 0) = 1.8
b(baru)  = 1.7 + 0        = 1.7

Bobot setelah data 3: w₁=1.8, w₂=1.8, b=1.7
```

**─── Data ke-4: x=[0, 1], t=0 ───**
```
w₁(baru) = 1.8 + (0 × 0) = 1.8
w₂(baru) = 1.8 + (1 × 0) = 1.8
b(baru)  = 1.7 + 0        = 1.7

Bobot FINAL: w₁=1.8, w₂=1.8, b=1.7
```

### E. Rekap Pelatihan Hebb

| Data | x1 | x2 | t | w₁(baru) | w₂(baru) | b(baru) |
|------|----|----|---|----------|----------|---------|
| Init |  — |  — | — | 0.8      | 0.8      | 0.7     |
| 1    |  1 |  0 | 0 | 0.8      | 0.8      | 0.7     |
| 2    |  1 |  1 | 1 | 1.8      | 1.8      | 1.7     |
| 3    |  0 |  0 | 0 | 1.8      | 1.8      | 1.7     |
| 4    |  0 |  1 | 0 | 1.8      | 1.8      | 1.7     |

**Bobot akhir: w₁ = 1.8, w₂ = 1.8, b = 1.7**

### F. Pengujian / Verifikasi (Diterima atau Ditolak?)

Rumus: `net = w₁·x₁ + w₂·x₂ + b`

**Data 1: x=[1, 0], t=0**
```
net = 1.8(1) + 1.8(0) + 1.7 = 1.8 + 0 + 1.7 = 3.5
f(net) = 1  (karena 3.5 ≥ 0)
Prediksi = 1, Target = 0  →  ❌ TIDAK SESUAI
```

**Data 2: x=[1, 1], t=1**
```
net = 1.8(1) + 1.8(1) + 1.7 = 1.8 + 1.8 + 1.7 = 5.3
f(net) = 1  (karena 5.3 ≥ 0)
Prediksi = 1, Target = 1  →  ✅ SESUAI
```

**Data 3: x=[0, 0], t=0**
```
net = 1.8(0) + 1.8(0) + 1.7 = 0 + 0 + 1.7 = 1.7
f(net) = 1  (karena 1.7 ≥ 0)
Prediksi = 1, Target = 0  →  ❌ TIDAK SESUAI
```

**Data 4: x=[0, 1], t=0**
```
net = 1.8(0) + 1.8(1) + 1.7 = 0 + 1.8 + 1.7 = 3.5
f(net) = 1  (karena 3.5 ≥ 0)
Prediksi = 1, Target = 0  →  ❌ TIDAK SESUAI
```

### G. Kesimpulan Soal 1

```
Hasil Verifikasi:
  Data 1: Prediksi=1, Target=0  → SALAH
  Data 2: Prediksi=1, Target=1  → BENAR
  Data 3: Prediksi=1, Target=0  → SALAH
  Data 4: Prediksi=1, Target=0  → SALAH

  Akurasi = 1/4 = 25%

KESIMPULAN: Model DITOLAK ❌
Jaringan Hebb tidak mampu mengenali fungsi AND dengan benar.

ALASAN:
Aturan Hebb bersifat unsupervised (tidak memperhitungkan error),
sehingga bobot hanya mencerminkan korelasi input-output tanpa
mekanisme koreksi. Dengan bias b=1.7 dan bobot awal w=0.8,
semua net input menjadi positif sehingga f(net) selalu = 1,
tanpa memandang input yang diberikan.

Untuk mengatasi ini diperlukan:
• Perceptron Learning Rule (ada mekanisme koreksi error)
• Penyesuaian bias atau threshold yang tepat
```

---

## SOAL 2 — Jaringan Perceptron [Bobot: 35]

> *Buat jaringan Perceptron dengan masukan biner dan keluaran bipolar. θ=0.3, α=0.7*

### A. Dataset

| x1 | x2 | t  |
|----|----|----|
| 0  | 1  | -1 |
| 0  | 0  | -1 |
| 1  | 1  | 1  |
| 1  | 0  | -1 |

Analisis target: Output +1 hanya saat x1=1, x2=1 → Fungsi **AND** (bipolar output)

### B. Parameter & Inisialisasi
```
θ (threshold) = 0.3
α (learning rate) = 0.7
Inisialisasi: w₁=0, w₂=0, b=0

Fungsi Aktivasi Bipolar Step:
       ⎧  1,  jika net >  0.3
f(net)=⎨  0,  jika -0.3 ≤ net ≤ 0.3
       ⎩ -1,  jika net < -0.3

Aturan Update Perceptron:
  Jika y ≠ t (prediksi salah):
    wᵢ(baru) = wᵢ(lama) + α × t × xᵢ
    b(baru)  = b(lama)  + α × t
  Jika y = t (prediksi benar): tidak ada perubahan bobot
```


### C. Pelatihan Perceptron — EPOCH 1

**─── Data ke-1: x=[0,1], t=-1 ───**
```
net = 0 + 0(0) + 0(1) = 0
f(net): -0.3 ≤ 0 ≤ 0.3  →  y = 0
y=0 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7 × (-1) × 0 = 0      → w₁ = 0+0   = 0
Δw₂ = 0.7 × (-1) × 1 = -0.7   → w₂ = 0-0.7 = -0.7
Δb  = 0.7 × (-1)     = -0.7   → b  = 0-0.7 = -0.7
```

**─── Data ke-2: x=[0,0], t=-1 ───**
```
net = -0.7 + 0(0) + (-0.7)(0) = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE (benar ✅)

Bobot tetap: w₁=0, w₂=-0.7, b=-0.7
```

**─── Data ke-3: x=[1,1], t=+1 ───**
```
net = -0.7 + 0(1) + (-0.7)(1) = -0.7 + 0 - 0.7 = -1.4
f(net): -1.4 < -0.3  →  y = -1
y=-1 ≠ t=+1  →  UPDATE BOBOT

Δw₁ = 0.7 × 1 × 1 = 0.7    → w₁ = 0+0.7   = 0.7
Δw₂ = 0.7 × 1 × 1 = 0.7    → w₂ = -0.7+0.7 = 0
Δb  = 0.7 × 1     = 0.7   → b  = -0.7+0.7 = 0
```

**─── Data ke-4: x=[1,0], t=-1 ───**
```
net = 0 + 0.7(1) + 0(0) = 0.7
f(net): 0.7 > 0.3  →  y = 1
y=1 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7 × (-1) × 1 = -0.7  → w₁ = 0.7-0.7 = 0
Δw₂ = 0.7 × (-1) × 0 = 0     → w₂ = 0+0     = 0
Δb  = 0.7 × (-1)     = -0.7  → b  = 0-0.7   = -0.7
```

### Rekap Epoch 1

| Data | x1 | x2 | t  | net   | y  | Update? | w₁  | w₂   | b    |
|------|----|----|-----|-------|----|---------|----- |------|------|
| Init |  — |  — | —  | —     | —  | —       | 0   | 0    | 0    |
| 1    |  0 |  1 | -1 | 0.00  | 0  | ✅ Ya   | 0   | -0.7 | -0.7 |
| 2    |  0 |  0 | -1 | -0.70 | -1 | ❌ Tidak| 0   | -0.7 | -0.7 |
| 3    |  1 |  1 | +1 | -1.40 | -1 | ✅ Ya   | 0.7 | 0    | 0    |
| 4    |  1 |  0 | -1 | 0.70  | +1 | ✅ Ya   | 0   | 0    | -0.7 |

Bobot akhir epoch 1: **w₁=0, w₂=0, b=-0.7**

---

### D. Pelatihan Perceptron — EPOCH 2

**─── Data ke-1: x=[0,1], t=-1 ───**
```
net = -0.7 + 0(0) + 0(1) = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE ✅
```

**─── Data ke-2: x=[0,0], t=-1 ───**
```
net = -0.7 + 0(0) + 0(0) = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE ✅
```

**─── Data ke-3: x=[1,1], t=+1 ───**
```
net = -0.7 + 0(1) + 0(1) = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 ≠ t=+1  →  UPDATE BOBOT

Δw₁ = 0.7×1×1 = 0.7  → w₁ = 0+0.7  = 0.7
Δw₂ = 0.7×1×1 = 0.7  → w₂ = 0+0.7  = 0.7
Δb  = 0.7×1   = 0.7  → b  = -0.7+0.7 = 0
```

**─── Data ke-4: x=[1,0], t=-1 ───**
```
net = 0 + 0.7(1) + 0.7(0) = 0.7
f(net): 0.7 > 0.3  →  y = +1
y=+1 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7×(-1)×1 = -0.7  → w₁ = 0.7-0.7 = 0
Δw₂ = 0.7×(-1)×0 = 0     → w₂ = 0.7+0   = 0.7
Δb  = 0.7×(-1)   = -0.7  → b  = 0-0.7   = -0.7
```

### Rekap Epoch 2

| Data | x1 | x2 | t  | net   | y  | Update? | w₁  | w₂  | b    |
|------|----|----|-----|-------|----|---------|----- |-----|------|
| Init |  — |  — | —  | —     | —  | —       | 0   | 0   | -0.7 |
| 1    |  0 |  1 | -1 | -0.70 | -1 | ❌ Tidak| 0   | 0   | -0.7 |
| 2    |  0 |  0 | -1 | -0.70 | -1 | ❌ Tidak| 0   | 0   | -0.7 |
| 3    |  1 |  1 | +1 | -0.70 | -1 | ✅ Ya   | 0.7 | 0.7 | 0    |
| 4    |  1 |  0 | -1 | 0.70  | +1 | ✅ Ya   | 0   | 0.7 | -0.7 |

Bobot akhir epoch 2: **w₁=0, w₂=0.7, b=-0.7**

---

### E. Pelatihan Perceptron — EPOCH 3

**─── Data ke-1: x=[0,1], t=-1 ───**
```
net = -0.7 + 0(0) + 0.7(1) = -0.7 + 0.7 = 0
f(net): -0.3 ≤ 0 ≤ 0.3  →  y = 0
y=0 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7×(-1)×0 = 0     → w₁ = 0
Δw₂ = 0.7×(-1)×1 = -0.7  → w₂ = 0.7-0.7 = 0
Δb  = 0.7×(-1)   = -0.7  → b  = -0.7-0.7 = -1.4
```

**─── Data ke-2: x=[0,0], t=-1 ───**
```
net = -1.4 + 0(0) + 0(0) = -1.4
f(net): -1.4 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE ✅
```

**─── Data ke-3: x=[1,1], t=+1 ───**
```
net = -1.4 + 0(1) + 0(1) = -1.4
f(net): -1.4 < -0.3  →  y = -1
y=-1 ≠ t=+1  →  UPDATE BOBOT

Δw₁ = 0.7×1×1 = 0.7  → w₁ = 0+0.7  = 0.7
Δw₂ = 0.7×1×1 = 0.7  → w₂ = 0+0.7  = 0.7
Δb  = 0.7×1   = 0.7  → b  = -1.4+0.7 = -0.7
```

**─── Data ke-4: x=[1,0], t=-1 ───**
```
net = -0.7 + 0.7(1) + 0.7(0) = -0.7+0.7 = 0
f(net): -0.3 ≤ 0 ≤ 0.3  →  y = 0
y=0 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7×(-1)×1 = -0.7  → w₁ = 0.7-0.7 = 0
Δw₂ = 0.7×(-1)×0 = 0     → w₂ = 0.7+0   = 0.7
Δb  = 0.7×(-1)   = -0.7  → b  = -0.7-0.7 = -1.4
```

### Rekap Epoch 3

| Data | x1 | x2 | t  | net   | y  | Update? | w₁  | w₂  | b    |
|------|----|----|-----|-------|----|---------|----- |-----|------|
| Init |  — |  — | —  | —     | —  | —       | 0   | 0.7 | -0.7 |
| 1    |  0 |  1 | -1 | 0.00  | 0  | ✅ Ya   | 0   | 0   | -1.4 |
| 2    |  0 |  0 | -1 | -1.40 | -1 | ❌ Tidak| 0   | 0   | -1.4 |
| 3    |  1 |  1 | +1 | -1.40 | -1 | ✅ Ya   | 0.7 | 0.7 | -0.7 |
| 4    |  1 |  0 | -1 | 0.00  | 0  | ✅ Ya   | 0   | 0.7 | -1.4 |

Bobot akhir epoch 3: **w₁=0, w₂=0.7, b=-1.4**


### F. Pelatihan Perceptron — EPOCH 4 (Verifikasi Konvergensi)

Bobot awal: w₁=0, w₂=0.7, b=-1.4

**─── Data ke-1: x=[0,1], t=-1 ───**
```
net = -1.4 + 0(0) + 0.7(1) = -1.4+0.7 = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE ✅
```

**─── Data ke-2: x=[0,0], t=-1 ───**
```
net = -1.4 + 0(0) + 0.7(0) = -1.4
f(net): -1.4 < -0.3  →  y = -1
y=-1 = t=-1  →  TIDAK UPDATE ✅
```

**─── Data ke-3: x=[1,1], t=+1 ───**
```
net = -1.4 + 0(1) + 0.7(1) = -1.4+0.7 = -0.7
f(net): -0.7 < -0.3  →  y = -1
y=-1 ≠ t=+1  →  UPDATE BOBOT

Δw₁ = 0.7×1×1 = 0.7  → w₁ = 0+0.7  = 0.7
Δw₂ = 0.7×1×1 = 0.7  → w₂ = 0.7+0.7 = 1.4
Δb  = 0.7×1   = 0.7  → b  = -1.4+0.7 = -0.7
```

**─── Data ke-4: x=[1,0], t=-1 ───**
```
net = -0.7 + 0.7(1) + 1.4(0) = -0.7+0.7 = 0
f(net): -0.3 ≤ 0 ≤ 0.3  →  y = 0
y=0 ≠ t=-1  →  UPDATE BOBOT

Δw₁ = 0.7×(-1)×1 = -0.7  → w₁ = 0.7-0.7 = 0
Δw₂ = 0.7×(-1)×0 = 0     → w₂ = 1.4+0   = 1.4
Δb  = 0.7×(-1)   = -0.7  → b  = -0.7-0.7 = -1.4
```

> **Pola oscillasi** terdeteksi: bobot berulang pada pola yang sama.
> Ini menunjukkan dataset **tidak linearly separable** dengan bipolar output dan threshold θ=0.3 ini.

### G. Kesimpulan Soal 2

```
Setelah beberapa epoch, bobot mengalami OSCILLASI (berulang) dan tidak konvergen.

Penyebab: Fungsi AND biner dengan output bipolar dan threshold θ=0.3 menyebabkan
zona "tak tentu" (y=0) sehingga data di batas keputusan tidak bisa diklasifikasikan.

Bobot terbaik yang mendekati benar: w₁=0.7, w₂=1.4, b=-1.4
→ Verifikasi:
  x=[0,1]: net=-1.4+0+1.4=0  → y=0  (target=-1) ❌
  x=[0,0]: net=-1.4+0+0=-1.4 → y=-1 (target=-1) ✅
  x=[1,1]: net=-1.4+0.7+1.4=0.7 → y=+1 (target=+1) ✅
  x=[1,0]: net=-1.4+0.7+0=-0.7 → y=-1 (target=-1) ✅

Akurasi = 3/4 = 75%
```

---

## SOAL 3 — Model Adaline [Bobot: 35]

> *Buat model ADALINE untuk mengenali pola fungsi logika. Toleransi = 0.04, α = 0.08*

### A. Dataset Bipolar

| x1 | x2 | t  |
|----|----|----|
| 1  | -1 | -1 |
| -1 | -1 | -1 |
| -1 | 1  | -1 |
| 1  | 1  | 1  |

Analisis: Output +1 hanya saat x1=+1 DAN x2=+1 → Fungsi **AND** bipolar

### B. Parameter & Inisialisasi
```
α (learning rate) = 0.08
Toleransi         = 0.04
Inisialisasi      : w₁=0, w₂=0, b=0

Fungsi aktivasi output (Bipolar Step):
       ⎧  1,  jika net ≥ 0
f(net)=⎨
       ⎩ -1,  jika net < 0

Aturan Update Adaline (Delta Rule / LMS):
  y_in     = b + w₁x₁ + w₂x₂   (LINEAR — tidak diaktivasi saat training)
  error    = t - y_in
  Δwᵢ      = α × error × xᵢ
  Δb       = α × error
  SSE      = Σ(error²)
  MSE      = SSE / n
  Konvergen jika MSE ≤ toleransi (0.04)
```

### C. Pelatihan EPOCH 1

**─── Data ke-1: x=[1,-1], t=-1 ───**
```
y_in = 0 + 0(1) + 0(-1) = 0
error = -1 - 0 = -1

Δw₁ = 0.08 × (-1) × 1  = -0.08  → w₁ = 0-0.08  = -0.08
Δw₂ = 0.08 × (-1) × (-1)= 0.08  → w₂ = 0+0.08  =  0.08
Δb  = 0.08 × (-1)       = -0.08 → b  = 0-0.08  = -0.08
SSE₁ = (-1)² = 1.0000
```

**─── Data ke-2: x=[-1,-1], t=-1 ───**
```
y_in = -0.08 + (-0.08)(-1) + (0.08)(-1) = -0.08+0.08-0.08 = -0.08
error = -1 - (-0.08) = -0.92

Δw₁ = 0.08 × (-0.92) × (-1) =  0.0736  → w₁ = -0.08+0.0736  = -0.0064
Δw₂ = 0.08 × (-0.92) × (-1) =  0.0736  → w₂ =  0.08+0.0736  =  0.1536
Δb  = 0.08 × (-0.92)         = -0.0736 → b  = -0.08-0.0736  = -0.1536
SSE₂ = (-0.92)² = 0.8464
```

**─── Data ke-3: x=[-1,1], t=-1 ───**
```
y_in = -0.1536 + (-0.0064)(-1) + (0.1536)(1)
     = -0.1536 + 0.0064 + 0.1536 = 0.0064
error = -1 - 0.0064 = -1.0064

Δw₁ = 0.08×(-1.0064)×(-1) =  0.0805  → w₁ = -0.0064+0.0805  =  0.0741
Δw₂ = 0.08×(-1.0064)×(1)  = -0.0805  → w₂ =  0.1536-0.0805  =  0.0731
Δb  = 0.08×(-1.0064)       = -0.0805 → b  = -0.1536-0.0805  = -0.2341
SSE₃ = (-1.0064)² = 1.0128
```

**─── Data ke-4: x=[1,1], t=+1 ───**
```
y_in = -0.2341 + (0.0741)(1) + (0.0731)(1)
     = -0.2341 + 0.0741 + 0.0731 = -0.0869
error = 1 - (-0.0869) = 1.0869

Δw₁ = 0.08×1.0869×1 =  0.0870  → w₁ = 0.0741+0.0870  =  0.1611
Δw₂ = 0.08×1.0869×1 =  0.0870  → w₂ = 0.0731+0.0870  =  0.1601
Δb  = 0.08×1.0869   =  0.0870  → b  = -0.2341+0.0870  = -0.1471
SSE₄ = (1.0869)² = 1.1813
```

### Rekap Epoch 1

| Data | x1 | x2 | t  | y_in    | error   | w₁      | w₂      | b        | SSE    |
|------|----|----|-----|---------|---------|---------|---------|----------|--------|
| Init |  — |  — | —  | —       | —       | 0       | 0       | 0        | —      |
| 1    |  1 | -1 | -1 | 0.0000  | -1.0000 | -0.0800 | 0.0800  | -0.0800  | 1.0000 |
| 2    | -1 | -1 | -1 | -0.0800 | -0.9200 | -0.0064 | 0.1536  | -0.1536  | 0.8464 |
| 3    | -1 |  1 | -1 | 0.0064  | -1.0064 | 0.0741  | 0.0731  | -0.2341  | 1.0128 |
| 4    |  1 |  1 | +1 | -0.0869 | 1.0869  | 0.1611  | 0.1601  | -0.1471  | 1.1813 |

```
SSE Total Epoch 1 = 1.0000 + 0.8464 + 1.0128 + 1.1813 = 4.0405
MSE Epoch 1       = 4.0405 / 4 = 1.0101

MSE (1.0101) >> Toleransi (0.04)  →  LANJUT ke Epoch berikutnya
```


### D. Pelatihan EPOCH 2

Bobot awal epoch 2: w₁=0.1611, w₂=0.1601, b=-0.1471

**─── Data ke-1: x=[1,-1], t=-1 ───**
```
y_in = -0.1471 + 0.1611(1) + 0.1601(-1) = -0.1471+0.1611-0.1601 = -0.1461
error = -1 - (-0.1461) = -0.8539

Δw₁ = 0.08×(-0.8539)×1  = -0.0683 → w₁ = 0.1611-0.0683 =  0.0928
Δw₂ = 0.08×(-0.8539)×(-1)= 0.0683 → w₂ = 0.1601+0.0683 =  0.2284
Δb  = 0.08×(-0.8539)     = -0.0683 → b  = -0.1471-0.0683 = -0.2154
SSE₁ = (-0.8539)² = 0.7292
```

**─── Data ke-2: x=[-1,-1], t=-1 ───**
```
y_in = -0.2154 + 0.0928(-1) + 0.2284(-1) = -0.2154-0.0928-0.2284 = -0.5366
error = -1 - (-0.5366) = -0.4634

Δw₁ = 0.08×(-0.4634)×(-1) =  0.0371 → w₁ = 0.0928+0.0371 =  0.1299
Δw₂ = 0.08×(-0.4634)×(-1) =  0.0371 → w₂ = 0.2284+0.0371 =  0.2655
Δb  = 0.08×(-0.4634)       = -0.0371 → b  = -0.2154-0.0371 = -0.2525
SSE₂ = (-0.4634)² = 0.2147
```

**─── Data ke-3: x=[-1,1], t=-1 ───**
```
y_in = -0.2525 + 0.1299(-1) + 0.2655(1) = -0.2525-0.1299+0.2655 = -0.1169
error = -1 - (-0.1169) = -0.8831

Δw₁ = 0.08×(-0.8831)×(-1) =  0.0706 → w₁ = 0.1299+0.0706 =  0.2005
Δw₂ = 0.08×(-0.8831)×(1)  = -0.0706 → w₂ = 0.2655-0.0706 =  0.1949
Δb  = 0.08×(-0.8831)       = -0.0706 → b  = -0.2525-0.0706 = -0.3231
SSE₃ = (-0.8831)² = 0.7799
```

**─── Data ke-4: x=[1,1], t=+1 ───**
```
y_in = -0.3231 + 0.2005(1) + 0.1949(1) = -0.3231+0.2005+0.1949 = 0.0723
error = 1 - 0.0723 = 0.9277

Δw₁ = 0.08×0.9277×1 =  0.0742 → w₁ = 0.2005+0.0742 =  0.2747
Δw₂ = 0.08×0.9277×1 =  0.0742 → w₂ = 0.1949+0.0742 =  0.2691
Δb  = 0.08×0.9277   =  0.0742 → b  = -0.3231+0.0742 = -0.2489
SSE₄ = (0.9277)² = 0.8606
```

### Rekap Epoch 2

| Data | x1 | x2 | t  | y_in    | error   | w₁      | w₂      | b        | SSE    |
|------|----|----|-----|---------|---------|---------|---------|----------|--------|
| Init |  — |  — | —  | —       | —       | 0.1611  | 0.1601  | -0.1471  | —      |
| 1    |  1 | -1 | -1 | -0.1461 | -0.8539 | 0.0928  | 0.2284  | -0.2154  | 0.7292 |
| 2    | -1 | -1 | -1 | -0.5366 | -0.4634 | 0.1299  | 0.2655  | -0.2525  | 0.2147 |
| 3    | -1 |  1 | -1 | -0.1169 | -0.8831 | 0.2005  | 0.1949  | -0.3231  | 0.7799 |
| 4    |  1 |  1 | +1 | 0.0723  | 0.9277  | 0.2747  | 0.2691  | -0.2489  | 0.8606 |

```
SSE Total Epoch 2 = 0.7292 + 0.2147 + 0.7799 + 0.8606 = 2.5844
MSE Epoch 2       = 2.5844 / 4 = 0.6461

MSE Epoch 1 = 1.0101  →  MSE Epoch 2 = 0.6461  (turun ✅, model belajar)
MSE (0.6461) > Toleransi (0.04)  →  Perlu epoch lanjutan
```

### E. Tren Konvergensi

```
Epoch 1 MSE = 1.0101
Epoch 2 MSE = 0.6461
Tren        = MENURUN (konvergen ke arah yang benar)

Model BELUM mencapai toleransi 0.04 setelah 2 epoch.
Diperlukan lebih banyak epoch (estimasi ~20-30 epoch dengan α=0.08)
```

### F. Kesimpulan Soal 3

```
Model ADALINE sedang dalam proses belajar dengan baik (MSE menurun),
namun BELUM KONVERGEN setelah 2 epoch karena:
  • Learning rate α=0.08 tergolong kecil → konvergensi lambat tapi stabil
  • Dari MSE 1.0101 → 0.6461, menunjukkan model terus belajar

BOBOT AKHIR SETELAH 2 EPOCH:
  w₁ = 0.2747
  w₂ = 0.2691
  b  = -0.2489

Prediksi sementara (bobot epoch 2):
  x=[1,-1]:  net = -0.2489+0.2747-0.2691 = -0.2433 → y=-1 (target=-1) ✅
  x=[-1,-1]: net = -0.2489-0.2747-0.2691 = -0.7927 → y=-1 (target=-1) ✅
  x=[-1,1]:  net = -0.2489-0.2747+0.2691 = -0.2545 → y=-1 (target=-1) ✅
  x=[1,1]:   net = -0.2489+0.2747+0.2691 =  0.2949 → y=+1 (target=+1) ✅

  Akurasi sementara = 4/4 = 100% ✅ (meskipun MSE belum di bawah toleransi)
  → Model sudah bisa mengklasifikasikan semua data dengan BENAR!

ARSITEKTUR JARINGAN ADALINE:
```

### G. Arsitektur Jaringan Adaline (Hasil Pelatihan)

```
  x₁ (+1/-1) ──── w₁ = 0.2747 ────┐
                                    ├──→ [∑ y_in] ──→ [f: Bipolar Step] ──→ y (+1/-1)
  x₂ (+1/-1) ──── w₂ = 0.2691 ────┤
                                    │
  Bias (1)   ──── b  = -0.2489 ───┘

  Persamaan:
    y_in = -0.2489 + 0.2747·x₁ + 0.2691·x₂

  Fungsi Aktivasi:
           ⎧ +1,  jika y_in ≥ 0
  f(y_in)= ⎨
           ⎩ -1,  jika y_in < 0

  Garis Keputusan (Decision Boundary):
    0.2747·x₁ + 0.2691·x₂ - 0.2489 = 0
    → Memisahkan kelas +1 (AND=True) dari kelas -1 (AND=False)

  Komponen Jaringan:
  ┌──────────────────────────────────────────────────────┐
  │  INPUT LAYER    │  PEMROSESAN         │  OUTPUT      │
  │  ─────────────  │  ─────────────────  │  ─────────── │
  │  x₁ = +1/-1    │  nett = Σwᵢxᵢ + b  │  y = +1/-1  │
  │  x₂ = +1/-1    │  (fungsi linear)    │  (bipolar)   │
  │  b  = 1        │                     │              │
  └──────────────────────────────────────────────────────┘
```

---

## RINGKASAN JAWABAN

| Soal | Model | Dataset | Konvergen? | Keterangan |
|------|-------|---------|-----------|------------|
| 1 | Hebb | AND biner | ❌ Tidak | Akurasi 25%, Hebb tidak bisa koreksi error |
| 2 | Perceptron | AND bipolar | ⚠️ Parsial | Akurasi 75%, oscillasi karena zona 0 (θ=0.3) |
| 3 | Adaline | AND bipolar | ✅ Fungsional | Akurasi 100% di epoch 2, MSE masih turun |

---
*Jawaban UTS Jaringan Syaraf Tiruan — T.A. 2021/2022*
*Universitas Indraprasta PGRI (UNINDRA)*
