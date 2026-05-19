# JAWABAN UTS JARINGAN SYARAF TIRUAN
**Universitas Indraprasta PGRI (UNINDRA)**
**Fakultas Teknik dan Ilmu Komputer**
**Mata Kuliah : Jaringan Syaraf Tiruan (+)**
**Tahun Akademik : 2024/2025 | Kamis, 8 Mei 2025**

---

## SOAL 1 — Arsitektur Jaringan Syaraf Tiruan [Bobot: 20]

> *Jaringan syaraf tiruan ditentukan oleh 3 hal utama, salah satunya arsitektur jaringan. Jelaskan pemahaman anda tentang arsitektur jaringan yang anda ketahui dan buatlah analogi dengan jaringan syaraf pada manusia!*

### A. Tiga Hal Utama yang Menentukan JST
1. **Arsitektur Jaringan** — susunan neuron dan cara koneksi antar layer
2. **Metode Pelatihan / Learning Rule** — cara bobot diperbarui (Hebb, Delta Rule, Backpropagation, dll.)
3. **Fungsi Aktivasi** — fungsi yang menentukan output neuron (Step, Sigmoid, ReLU, dll.)

### B. Jenis-Jenis Arsitektur Jaringan

| Arsitektur | Deskripsi | Contoh Model |
|------------|-----------|--------------|
| **Single Layer** | Hanya ada layer input dan output, tidak ada hidden layer | Perceptron, Adaline, MADALINE |
| **Multilayer (MLP)** | Terdapat satu atau lebih hidden layer antara input dan output | Backpropagation Network |
| **Recurrent** | Terdapat koneksi umpan balik (feedback) dari output ke input | Hopfield Network, Elman Network |

### C. Penjelasan Arsitektur

**Single Layer Feedforward:**
- Sinyal mengalir satu arah: input → output
- Cocok untuk masalah yang linearly separable

**Multilayer Feedforward:**
- Sinyal mengalir: input → hidden layer(s) → output
- Hidden layer memungkinkan pembelajaran pola non-linear
- Semakin banyak hidden layer = semakin kompleks pola yang bisa dipelajari

**Recurrent Network:**
- Output dapat menjadi input kembali (ada loop/feedback)
- Mampu memproses data sekuensial/temporal


### D. Analogi dengan Jaringan Syaraf Manusia

| Komponen JST | Analogi Syaraf Manusia |
|--------------|----------------------|
| **Neuron / Node** | Sel saraf (neuron biologis) |
| **Input (xᵢ)** | Dendrit — menerima sinyal dari luar |
| **Bobot (wᵢ)** | Kekuatan sinapsis — seberapa kuat sinyal diteruskan |
| **Fungsi penjumlahan (∑)** | Soma / badan sel — mengintegrasikan semua sinyal masuk |
| **Fungsi Aktivasi f(net)** | Axon hillock — menentukan apakah neuron "menembak" atau tidak |
| **Output (y)** | Axon terminal — mengirimkan sinyal ke neuron berikutnya |
| **Bias (b)** | Ambang batas internal sel saraf (threshold potensial) |
| **Layer tersembunyi** | Jaringan interneuron di otak yang mengolah informasi |

**Ilustrasi Analogi:**
```
[Panca Indera] → [Dendrit/Input] → [Soma/Penjumlahan] → [Axon/Output] → [Respons]
      ↕                                     ↕
[xᵢ · wᵢ]   →     [Σ xᵢwᵢ + b]    →    [f(net)]       →      [y]
```

> Seperti otak manusia yang belajar dari pengalaman dengan memperkuat sinapsis yang sering digunakan (Hebb's Law), JST belajar dengan **memperbarui bobot** berdasarkan kesalahan prediksi.

---

## SOAL 2 — Penjelasan Komponen Neuron Buatan [Bobot: 25]

> *Jelaskan setiap bagian dari gambar (x₁..xₙ, w₁..wₙ, nett, f(nett), y, Bias b) dan tuliskan cara kerjanya!*

### A. Penjelasan Setiap Komponen

| Komponen | Nama | Penjelasan |
|----------|------|------------|
| **x₁, x₂, ..., xₙ** | Input | Sinyal masukan dari luar atau dari neuron sebelumnya. Nilainya bisa biner (0/1), bipolar (-1/+1), atau real. |
| **w₁, w₂, ..., wₙ** | Bobot (Weight) | Nilai numerik yang mewakili kekuatan koneksi antara input dan neuron. Bobot positif = eksitatori, negatif = inhibitori. |
| **b (Bias)** | Bias | Nilai konstan tambahan yang memungkinkan neuron untuk "bergeser" dari nol. Setara dengan intersep dalam regresi linear. Selalu bernilai 1 dikalikan bobotnya. |
| **nett** | Net Input / Aktivasi Total | Hasil penjumlahan berbobot dari semua input ditambah bias. Ini adalah nilai "mentah" sebelum diaktivasi. |
| **f(nett)** | Fungsi Aktivasi | Fungsi yang mentransformasi nilai nett menjadi output. Menentukan apakah neuron "aktif" atau tidak. |
| **y** | Output | Hasil akhir neuron setelah melewati fungsi aktivasi. Nilai ini diteruskan ke neuron berikutnya atau menjadi output jaringan. |


### B. Rumus Net Input

```
nett = (x₁ × w₁) + (x₂ × w₂) + ... + (xₙ × wₙ) + b

       n
nett = Σ (xᵢ × wᵢ) + b
      i=1
```

### C. Cara Kerja Neuron (Step by Step)

```
LANGKAH 1 — Menerima Input:
  Neuron menerima sinyal x₁, x₂, ..., xₙ dari lingkungan atau neuron sebelumnya.

LANGKAH 2 — Perkalian dengan Bobot:
  Setiap input dikalikan dengan bobotnya masing-masing:
  → x₁·w₁,  x₂·w₂,  ...,  xₙ·wₙ

LANGKAH 3 — Penjumlahan (Fungsi Agregasi):
  Semua hasil perkalian dijumlahkan bersama bias:
  → nett = Σ(xᵢ·wᵢ) + b

LANGKAH 4 — Fungsi Aktivasi:
  Nilai nett dimasukkan ke fungsi aktivasi f(nett).
  Fungsi aktivasi yang umum digunakan:
  • Step Function   : y = 1 jika nett ≥ θ, y = 0 jika nett < θ
  • Sigmoid         : y = 1 / (1 + e^(-nett))
  • ReLU            : y = max(0, nett)
  • Bipolar Step    : y = +1 jika nett ≥ θ, y = -1 jika nett < θ

LANGKAH 5 — Output:
  Hasil f(nett) = y dikirim sebagai output neuron.
```

### D. Ilustrasi Alur Kerja

```
  x₁ ──(w₁)──┐
  x₂ ──(w₂)──┤
              ├──→ [ nett = Σxᵢwᵢ + b ] ──→ [ f(nett) ] ──→  y
  xₙ ──(wₙ)──┤
  b=1──(b) ───┘

  Contoh (n=3, x=[1,0,1], w=[0.5,-0.3,0.8], b=0.2):
  nett = (1×0.5) + (0×-0.3) + (1×0.8) + 0.2 = 1.5
  y    = f(1.5) = 1  (dengan Step Function θ=0.5)
```

---

## SOAL 3 — Arsitektur Multilayer Perceptron [Bobot: 15]

> *Gambarkan dan jelaskan setiap bagian dalam arsitektur multilayer perceptron!*

### A. Arsitektur MLP

```
  INPUT LAYER       HIDDEN LAYER 1     HIDDEN LAYER 2      OUTPUT LAYER
  ───────────       ──────────────     ──────────────      ────────────
    x₁  ●─────────→● h₁₁ ──────────→● h₂₁ ──────────→● y₁
        ╲  ╲  ╲    → ● h₁₂           → ● h₂₂           → ● y₂
    x₂  ●──╲──╲──→→ ● h₁₃           → ● h₂₃
        ╲   ╲  ╲   → ● h₁₄
    x₃  ●────╲──→→→ ● h₁₅
         ╲    ╲
    x₄  ●─────→───→ (semua input terhubung ke semua hidden neuron)
```

### B. Penjelasan Setiap Layer

**1. Input Layer (Layer Masukan)**
- Menerima data mentah dari luar (fitur-fitur dataset)
- Jumlah neuron = jumlah fitur input
- **Tidak melakukan komputasi**, hanya meneruskan nilai input ke layer berikutnya
- Contoh: jika dataset memiliki 3 fitur (x₁, x₂, x₃), maka input layer memiliki 3 neuron

**2. Hidden Layer (Layer Tersembunyi)**
- Terletak di antara input layer dan output layer
- Melakukan **transformasi non-linear** terhadap data
- Jumlah hidden layer dan neuron per layer ditentukan oleh desainer (hyperparameter)
- Semakin banyak hidden layer → jaringan semakin "dalam" (Deep Neural Network)
- Setiap neuron menghitung: `nett = Σ(xᵢ·wᵢ) + b`, lalu `f(nett)`
- Fungsi aktivasi yang umum: **ReLU, Sigmoid, Tanh**

**3. Output Layer (Layer Keluaran)**
- Layer terakhir yang menghasilkan prediksi/output jaringan
- Jumlah neuron = jumlah kelas (klasifikasi) atau 1 (regresi)
- Fungsi aktivasi output: **Sigmoid** (biner), **Softmax** (multi-kelas), **Linear** (regresi)

**4. Bobot dan Bias**
- Setiap koneksi antar neuron memiliki bobot (w) yang bisa dipelajari
- Bias memungkinkan pergeseran fungsi aktivasi
- Diperbarui menggunakan algoritma **Backpropagation + Gradient Descent**


### C. Cara Kerja MLP (Forward Pass & Backpropagation)

```
FORWARD PASS (kiri ke kanan):
  1. Data masuk ke Input Layer
  2. Sinyal dikalikan bobot, dijumlahkan, diaktivasi di setiap Hidden Layer
  3. Output Layer menghasilkan prediksi ŷ

BACKPROPAGATION (kanan ke kiri):
  1. Hitung error: E = ½(target - ŷ)²
  2. Hitung gradient error terhadap setiap bobot (chain rule)
  3. Update bobot: w = w - α × (∂E/∂w)
  4. Ulangi hingga konvergen
```

| Aspek | Single Layer Perceptron | Multilayer Perceptron (MLP) |
|-------|------------------------|----------------------------|
| Jumlah Layer | 2 (input + output) | 3+ (input + hidden(s) + output) |
| Kemampuan | Linearly separable only | Non-linear, kompleks |
| Fungsi Aktivasi | Step Function | Sigmoid, ReLU, Tanh |
| Algoritma Belajar | Perceptron Learning Rule | Backpropagation |
| Contoh Masalah | AND, OR | XOR, klasifikasi gambar, NLP |

---

## SOAL 4 — Pelatihan Adaline: (X1 AND X2) OR X3 [Bobot: 40]

> *Latihlah dataset logika (X1 AND X2) OR X3 dengan Adaline. epoch=2, α=1, toleransi=0.005*

### A. Dataset dan Target

Fungsi logika **(X1 AND X2) OR X3** dalam bipolar (-1 = False, +1 = True):

| No | X1 | X2 | X3 | X1 AND X2 | Target t = (X1∧X2)∨X3 |
|----|----|----|-----|-----------|----------------------|
| 1  | +1 | +1 | +1  | +1        | **+1** |
| 2  | +1 | +1 | -1  | +1        | **+1** |
| 3  | +1 | -1 | +1  | -1        | **+1** |
| 4  | +1 | -1 | -1  | -1        | **-1** |
| 5  | -1 | +1 | +1  | -1        | **+1** |
| 6  | -1 | +1 | -1  | -1        | **-1** |
| 7  | -1 | -1 | +1  | -1        | **+1** |
| 8  | -1 | -1 | -1  | -1        | **-1** |

### B. Parameter dan Inisialisasi
```
α (learning rate) = 1
Toleransi         = 0.005
Max Epoch         = 2
Inisialisasi      : w₁=0, w₂=0, w₃=0, b=0

Fungsi aktivasi (output akhir):
         ⎧ +1,  jika y_in ≥ 0
f(y_in)= ⎨
         ⎩ -1,  jika y_in < 0

Aturan update (Delta Rule / LMS):
  y_in    = b + w₁x₁ + w₂x₂ + w₃x₃   (linear, bukan diaktivasi saat training)
  Δwᵢ     = α × (t - y_in) × xᵢ
  Δb      = α × (t - y_in)
```


### C. Pelatihan EPOCH 1

**─── Data ke-1: x=[+1,+1,+1], t=+1 ───**
```
y_in = 0 + 0(1)+0(1)+0(1) = 0
error = t - y_in = 1 - 0 = 1

Δw₁ = 1 × 1 × 1 = 1     → w₁ = 0+1 = 1
Δw₂ = 1 × 1 × 1 = 1     → w₂ = 0+1 = 1
Δw₃ = 1 × 1 × 1 = 1     → w₃ = 0+1 = 1
Δb  = 1 × 1     = 1     → b  = 0+1 = 1
SSE₁ = (1)² = 1.0000
```

**─── Data ke-2: x=[+1,+1,-1], t=+1 ───**
```
y_in = 1 + 1(1)+1(1)+1(-1) = 1+1+1-1 = 2
error = 1 - 2 = -1

Δw₁ = 1×(-1)×1 = -1    → w₁ = 1-1 = 0
Δw₂ = 1×(-1)×1 = -1    → w₂ = 1-1 = 0
Δw₃ = 1×(-1)×(-1) = 1  → w₃ = 1+1 = 2
Δb  = 1×(-1)    = -1   → b  = 1-1 = 0
SSE₂ = (-1)² = 1.0000
```

**─── Data ke-3: x=[+1,-1,+1], t=+1 ───**
```
y_in = 0 + 0(1)+0(-1)+2(1) = 2
error = 1 - 2 = -1

Δw₁ = 1×(-1)×1  = -1   → w₁ = 0-1 = -1
Δw₂ = 1×(-1)×(-1) = 1  → w₂ = 0+1 = 1
Δw₃ = 1×(-1)×1  = -1   → w₃ = 2-1 = 1
Δb  = 1×(-1)    = -1   → b  = 0-1 = -1
SSE₃ = (-1)² = 1.0000
```

**─── Data ke-4: x=[+1,-1,-1], t=-1 ───**
```
y_in = -1 + (-1)(1)+1(-1)+1(-1) = -1-1-1-1 = -4
error = -1 - (-4) = 3

Δw₁ = 1×3×1   = 3    → w₁ = -1+3 = 2
Δw₂ = 1×3×(-1) = -3  → w₂ = 1-3 = -2
Δw₃ = 1×3×(-1) = -3  → w₃ = 1-3 = -2
Δb  = 1×3      = 3   → b  = -1+3 = 2
SSE₄ = (3)² = 9.0000
```

**─── Data ke-5: x=[-1,+1,+1], t=+1 ───**
```
y_in = 2 + 2(-1)+(-2)(1)+(-2)(1) = 2-2-2-2 = -4
error = 1 - (-4) = 5

Δw₁ = 1×5×(-1) = -5  → w₁ = 2-5 = -3
Δw₂ = 1×5×1    = 5   → w₂ = -2+5 = 3
Δw₃ = 1×5×1    = 5   → w₃ = -2+5 = 3
Δb  = 1×5      = 5   → b  = 2+5 = 7
SSE₅ = (5)² = 25.0000
```

**─── Data ke-6: x=[-1,+1,-1], t=-1 ───**
```
y_in = 7 + (-3)(-1)+3(1)+3(-1) = 7+3+3-3 = 10
error = -1 - 10 = -11

Δw₁ = 1×(-11)×(-1) = 11   → w₁ = -3+11 = 8
Δw₂ = 1×(-11)×1    = -11  → w₂ = 3-11 = -8
Δw₃ = 1×(-11)×(-1) = 11   → w₃ = 3+11 = 14
Δb  = 1×(-11)       = -11 → b  = 7-11 = -4
SSE₆ = (-11)² = 121.0000
```

**─── Data ke-7: x=[-1,-1,+1], t=+1 ───**
```
y_in = -4 + 8(-1)+(-8)(-1)+14(1) = -4-8+8+14 = 10
error = 1 - 10 = -9

Δw₁ = 1×(-9)×(-1) = 9   → w₁ = 8+9 = 17
Δw₂ = 1×(-9)×(-1) = 9   → w₂ = -8+9 = 1
Δw₃ = 1×(-9)×1    = -9  → w₃ = 14-9 = 5
Δb  = 1×(-9)       = -9 → b  = -4-9 = -13
SSE₇ = (-9)² = 81.0000
```

**─── Data ke-8: x=[-1,-1,-1], t=-1 ───**
```
y_in = -13 + 17(-1)+1(-1)+5(-1) = -13-17-1-5 = -36
error = -1 - (-36) = 35

Δw₁ = 1×35×(-1) = -35  → w₁ = 17-35 = -18
Δw₂ = 1×35×(-1) = -35  → w₂ = 1-35 = -34
Δw₃ = 1×35×(-1) = -35  → w₃ = 5-35 = -30
Δb  = 1×35      = 35   → b  = -13+35 = 22
SSE₈ = (35)² = 1225.0000
```


### Rekap Epoch 1

| Data | x₁ | x₂ | x₃ | t  | y_in | error | w₁  | w₂  | w₃  | b   | SSE    |
|------|----|----|-----|----|----- |-------|-----|-----|-----|-----|--------|
| Init | —  | —  | —   | —  | —    | —     | 0   | 0   | 0   | 0   | —      |
| 1    | +1 | +1 | +1  | +1 | 0    | 1     | 1   | 1   | 1   | 1   | 1.000  |
| 2    | +1 | +1 | -1  | +1 | 2    | -1    | 0   | 0   | 2   | 0   | 1.000  |
| 3    | +1 | -1 | +1  | +1 | 2    | -1    | -1  | 1   | 1   | -1  | 1.000  |
| 4    | +1 | -1 | -1  | -1 | -4   | 3     | 2   | -2  | -2  | 2   | 9.000  |
| 5    | -1 | +1 | +1  | +1 | -4   | 5     | -3  | 3   | 3   | 7   | 25.000 |
| 6    | -1 | +1 | -1  | -1 | 10   | -11   | 8   | -8  | 14  | -4  | 121.000|
| 7    | -1 | -1 | +1  | +1 | 10   | -9    | 17  | 1   | 5   | -13 | 81.000 |
| 8    | -1 | -1 | -1  | -1 | -36  | 35    | -18 | -34 | -30 | 22  | 1225.000|

**Total SSE Epoch 1 = 1+1+1+9+25+121+81+1225 = 1464**
**MSE Epoch 1 = 1464 / 8 = 183.00**
> MSE = 183.00 >> toleransi 0.005 → **Lanjut Epoch 2**

---

### D. Pelatihan EPOCH 2

Bobot awal epoch 2: w₁=-18, w₂=-34, w₃=-30, b=22

**─── Data ke-1: x=[+1,+1,+1], t=+1 ───**
```
y_in = 22 + (-18)(1)+(-34)(1)+(-30)(1) = 22-18-34-30 = -60
error = 1 - (-60) = 61

Δw₁ = 1×61×1  = 61   → w₁ = -18+61 = 43
Δw₂ = 1×61×1  = 61   → w₂ = -34+61 = 27
Δw₃ = 1×61×1  = 61   → w₃ = -30+61 = 31
Δb  = 1×61    = 61   → b  = 22+61  = 83
SSE = 61² = 3721
```

**─── Data ke-2: x=[+1,+1,-1], t=+1 ───**
```
y_in = 83 + 43(1)+27(1)+31(-1) = 83+43+27-31 = 122
error = 1 - 122 = -121

Δw₁ = 1×(-121)×1  = -121  → w₁ = 43-121 = -78
Δw₂ = 1×(-121)×1  = -121  → w₂ = 27-121 = -94
Δw₃ = 1×(-121)×(-1) = 121 → w₃ = 31+121 = 152
Δb  = 1×(-121)     = -121 → b  = 83-121 = -38
SSE = (-121)² = 14641
```

> ⚠️ **Catatan:** Bobot meledak (exploding weights) karena learning rate α=1 terlalu besar untuk dataset ini. Dalam praktik nyata, α yang lebih kecil (mis. 0.01–0.1) diperlukan agar konvergen.

### E. Kesimpulan Pelatihan

```
Epoch 1 MSE = 183.00   → TIDAK konvergen (>> 0.005)
Epoch 2 MSE = sangat besar (bobot divergen karena α=1 terlalu besar)

KESIMPULAN:
Model TIDAK BERHASIL konvergen dalam 2 epoch dengan α=1 dan toleransi=0.005.
Penyebab: Learning rate α=1 terlalu besar menyebabkan overshoot pada setiap
update bobot, sehingga error justru membesar dari epoch ke epoch (divergen).

SARAN:
• Gunakan α yang lebih kecil (mis. α = 0.01 atau 0.1)
• Tambah jumlah epoch (mis. 1000 epoch)
• Normalisasi data input terlebih dahulu
```

Karena model **tidak berhasil**, arsitektur jaringan tidak dapat digambarkan sebagai model final.
Jika model berhasil (konvergen), arsitektur Adaline-nya adalah:

```
  x₁ (+1/-1) ──── w₁ ────┐
  x₂ (+1/-1) ──── w₂ ────┤──→ [∑ y_in = b + Σwᵢxᵢ] ──→ [f: Sign] ──→ y (+1/-1)
  x₃ (+1/-1) ──── w₃ ────┤
  Bias (1)   ──── b  ────┘

  Single layer, 3 input + 1 bias, 1 output
  Fungsi aktivasi: Bipolar Step (Sign function)
  Update: Delta Rule (LMS) — wᵢ += α(t - y_in)xᵢ
```

---
*Jawaban UTS Jaringan Syaraf Tiruan — T.A. 2024/2025*
*Universitas Indraprasta PGRI (UNINDRA)*
