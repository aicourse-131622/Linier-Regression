Saya sudah membaca file **Linier Regression.ipynb** yang Anda upload. Berikut penjelasan **detail setiap bagian kode** dari awal sampai akhir.

# 1. Import Library

```python
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score
import matplotlib.pyplot as plt
```

## Fungsi masing-masing library

### NumPy

```python
import numpy as np
```

Digunakan untuk:

* Operasi matematika
* Array numerik
* Membuat data acak

Contoh:

```python
np.random.randint(1,10,5)
```

menghasilkan angka acak.

---

### Pandas

```python
import pandas as pd
```

Digunakan untuk:

* Membuat tabel data (DataFrame)
* Membaca CSV/Excel
* Mengolah data

Contoh:

```python
pd.DataFrame(...)
```

---

### Linear Regression

```python
from sklearn.linear_model import LinearRegression
```

Digunakan untuk membuat model Regresi Linear.

Persamaan:

[
Y = \beta_0 + \beta_1X_1 + \beta_2X_2
]

---

### Train Test Split

```python
from sklearn.model_selection import train_test_split
```

Digunakan untuk membagi data menjadi:

* Data latih (training)
* Data uji (testing)

---

### Evaluasi

```python
from sklearn.metrics import mean_squared_error, r2_score
```

Digunakan untuk mengukur kualitas model.

---

### Visualisasi

```python
import matplotlib.pyplot as plt
```

Digunakan untuk membuat grafik.

---

# 2. Membuat Dataset Sintetis

```python
np.random.seed(42)
n = 100
```

## np.random.seed(42)

Digunakan agar hasil random selalu sama.

Misalnya hari ini dan besok dijalankan:

```python
np.random.randint(1,10,5)
```

hasilnya tetap sama.

Ini penting untuk reproduksibilitas penelitian.

---

## n = 100

Artinya:

```python
100 data rumah
```

akan dibuat.

---

# 3. Membuat Variabel Luas

```python
luas = np.random.randint(40, 200, n)
```

Membuat 100 angka acak antara:

```python
40 sampai 199
```

Contoh:

```python
[142, 87, 180, 65, ...]
```

Artinya:

* Rumah pertama = 142 m²
* Rumah kedua = 87 m²
* dst

---

# 4. Membuat Variabel Jumlah Kamar

```python
kamar = np.random.randint(1, 6, n)
```

Menghasilkan angka:

```python
1 sampai 5 kamar
```

Contoh:

```python
[2,4,3,1,5,...]
```

---

# 5. Membuat Harga Rumah

```python
harga = 200 + 2.5*luas + 15*kamar + np.random.normal(0, 20, n)
```

Ini bagian terpenting.

Persamaan yang digunakan:

[
Harga = 200 + 2.5(Luas) + 15(Kamar) + Error
]

---

## Komponen 1

```python
200
```

Harga dasar rumah.

---

## Komponen 2

```python
2.5 * luas
```

Setiap tambahan:

```python
1 m²
```

harga naik:

```python
2.5 juta
```

---

## Komponen 3

```python
15 * kamar
```

Setiap tambahan:

```python
1 kamar
```

harga naik:

```python
15 juta
```

---

## Komponen 4

```python
np.random.normal(0,20,n)
```

Menambahkan noise/error.

Misalnya:

```python
+5
-10
+18
```

agar data terlihat realistis.

Karena dunia nyata tidak selalu mengikuti rumus sempurna.

---

# 6. Membuat DataFrame

```python
df = pd.DataFrame({
    'luas_m2': luas,
    'jumlah_kamar': kamar,
    'harga_juta': harga
})
```

Hasilnya:

| luas_m2 | jumlah_kamar | harga_juta |
| ------- | ------------ | ---------- |
| 142     | 3            | 603        |
| 87      | 2            | 453        |
| 180     | 5            | 720        |

---

# 7. Menampilkan Data

```python
print("5 data pertama:")
print(df.head())
```

## head()

Menampilkan:

```python
5 baris pertama
```

Contoh:

| luas_m2 | jumlah_kamar | harga_juta |
| ------- | ------------ | ---------- |
| 142     | 3            | 603        |
| 87      | 2            | 453        |
| 180     | 5            | 720        |
| 65      | 1            | 380        |
| 90      | 4            | 510        |

---

# 8. Menentukan Fitur dan Target

```python
X = df[['luas_m2', 'jumlah_kamar']]
y = df['harga_juta']
```

## X

Variabel input.

```python
X
```

berisi:

| luas_m2 | jumlah_kamar |
| ------- | ------------ |
| 142     | 3            |
| 87      | 2            |
| 180     | 5            |

---

## y

Target yang ingin diprediksi.

```python
harga_juta
```

---

# 9. Membagi Data Training dan Testing

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42
)
```

## test_size=0.2

Artinya:

* 80% training
* 20% testing

Karena ada 100 data:

Training:

```python
80 data
```

Testing:

```python
20 data
```

---

# 10. Membuat Model

```python
model = LinearRegression()
```

Membuat objek regresi linear.

Belum belajar apa-apa.

Masih kosong.

---

# 11. Melatih Model

```python
model.fit(X_train, y_train)
```

Di sinilah proses Machine Learning terjadi.

Model belajar hubungan:

```text
Luas -> Harga
Kamar -> Harga
```

Model mencari:

```text
β₀
β₁
β₂
```

yang paling sesuai.

---

# 12. Menampilkan Persamaan Model

```python
print(f"\nIntercept (β₀) : {model.intercept_:.2f}")
print(f"Koefisien luas : {model.coef_[0]:.2f}")
print(f"Koefisien kamar : {model.coef_[1]:.2f}")
```

Misalnya hasil:

```text
Intercept : 197.21
Koefisien luas : 2.51
Koefisien kamar : 14.98
```

Maka model menemukan:

[
Harga = 197.21 + 2.51(Luas) + 14.98(Kamar)
]

Sangat dekat dengan rumus asli:

[
Harga = 200 + 2.5(Luas) + 15(Kamar)
]

Artinya model berhasil belajar pola data.

---

# 13. Prediksi Data Test

```python
y_pred = model.predict(X_test)
```

Model mencoba menebak harga rumah pada data yang belum pernah dilihat.

---

# 14. Menghitung MSE

```python
mse = mean_squared_error(y_test, y_pred)
```

Rumus:

[
MSE = \frac{\sum (Aktual - Prediksi)^2}{n}
]

Semakin kecil semakin baik.

---

# 15. Menghitung R²

```python
r2 = r2_score(y_test, y_pred)
```

Mengukur seberapa baik model menjelaskan data.

Nilai:

| R²  | Interpretasi |
| --- | ------------ |
| 0   | Buruk        |
| 0.5 | Lumayan      |
| 0.8 | Baik         |
| 1   | Sempurna     |

---

# 16. Menampilkan Hasil Evaluasi

```python
print(f"\nMSE  : {mse:.2f}")
print(f"RMSE : {np.sqrt(mse):.2f}")
print(f"R²   : {r2:.4f}")
```

### RMSE

```python
np.sqrt(mse)
```

Akar dari MSE.

Lebih mudah dipahami karena satuannya sama dengan harga rumah.

---

# 17. Prediksi Rumah Baru

```python
rumah_baru = pd.DataFrame({
    'luas_m2': [120],
    'jumlah_kamar': [3]
})
```

Membuat data rumah baru:

| luas_m2 | jumlah_kamar |
| ------- | ------------ |
| 120     | 3            |

---

## Prediksi

```python
prediksi = model.predict(rumah_baru)
```

Menghasilkan harga prediksi.

---

## Menampilkan

```python
print(
f"\nPrediksi harga rumah 120m2/3 kamar: Rp{prediksi[0]:.1f} juta"
)
```

Misalnya:

```text
Prediksi harga rumah 120m2/3 kamar: Rp543.4 juta
```

---

# 18. Visualisasi

```python
plt.figure(figsize=(8,4))
```

Membuat area grafik ukuran:

```text
8 x 4 inci
```

---

## Scatter Plot

```python
plt.scatter(
    y_test,
    y_pred,
    alpha=0.7,
    color='steelblue'
)
```

Menampilkan titik:

* Sumbu X = Harga Aktual
* Sumbu Y = Harga Prediksi

---

## Garis Ideal

```python
plt.plot(
[y_test.min(), y_test.max()],
[y_test.min(), y_test.max()],
'r--',
lw=2,
label='ideal'
)
```

Membuat garis merah putus-putus.

Jika semua titik berada tepat di garis ini:

```text
Prediksi = Aktual
```

artinya model sempurna.

---

## Label Sumbu

```python
plt.xlabel('Harga Aktual (juta)')
```

Sumbu X.

```python
plt.ylabel('Harga Prediksi (juta)')
```

Sumbu Y.

---

## Judul

```python
plt.title('Linier Regression -- Aktual vs Prediksi')
```

Judul grafik.

---

## Legend

```python
plt.legend()
```

Menampilkan keterangan grafik.

---

## Rapikan Layout

```python
plt.tight_layout()
```

Agar tulisan tidak terpotong.

---

## Tampilkan Grafik

```python
plt.show()
```

Menampilkan hasil visualisasi.

---

## Kesimpulan Alur Program

```text
1. Import library
        ↓
2. Buat data rumah sintetis
        ↓
3. Pisahkan fitur dan target
        ↓
4. Bagi data train-test
        ↓
5. Latih model regresi linear
        ↓
6. Dapatkan persamaan regresi
        ↓
7. Evaluasi akurasi model
        ↓
8. Prediksi harga rumah baru
        ↓
9. Visualisasikan hasil prediksi
```

Notebook ini merupakan contoh yang sangat baik untuk mempelajari dasar **Machine Learning (Supervised Learning)** karena mencakup seluruh alur kerja: **dataset → training → evaluasi → prediksi → visualisasi**.
