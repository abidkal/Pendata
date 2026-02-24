# Data Understanding

Data Understanding merupakan fase eksplorasi awal yang bertujuan mengenali karakteristik dan kondisi data sebelum diproses lebih lanjut. Data dapat berasal dari berbagai format, seperti XML, JSON, maupun basis data relasional. Sebelum analisis dilakukan, data perlu diperiksa dan dibersihkan agar hasil pengolahan dapat diandalkan.

## Konsep Dasar

### Kualitas dan Kebersihan Data

Keberadaan data yang tidak bersih (_dirty data_) dapat menurunkan akurasi hasil analisis. Beberapa masalah umum yang ditemui pada data mentah antara lain:

1. **Redudansi data**: Data yang tercatat lebih dari sekali sehingga menyebabkan duplikasi dalam dataset.
2. **Data tidak konsisten**: Data yang merepresentasikan informasi yang sama namun memiliki format atau nilai yang berbeda-beda.

Penilaian kualitas data dilakukan dengan memeriksa adanya _missing values_ dan baris duplikat. Secara umum, _missing values_ masih dapat ditoleransi apabila jumlahnya di bawah 10 persen dari keseluruhan data.

### Komponen Utama Memahami Data

Proses pemahaman data mencakup empat komponen yang saling berkaitan:

1. **Pengumpulan data awal**: Menghimpun data mentah dari berbagai sumber yang relevan.
2. **Deskripsi data**: Menjabarkan karakteristik umum dari data yang telah dikumpulkan.
3. **Eksplorasi data**: Mengidentifikasi pola dan keterkaitan awal antar variabel melalui statistik maupun visualisasi.
4. **Kualitas data**: Memverifikasi bahwa data telah memenuhi standar kelayakan untuk digunakan dalam pemodelan.

### Struktur Data dan Seleksi Fitur

Data tabular tersusun dalam bentuk baris (record) dan kolom (fitur). Tidak semua kolom yang tersedia diperlukan dalam analisis, sehingga dilakukan seleksi fitur untuk menyisakan hanya variabel yang relevan dan berkontribusi terhadap tujuan pemodelan.


# DATA UNDERSTANDING DAN EKSPLORASI DATA IRIS

Notebook ini berisi proses eksplorasi dataset Iris menggunakan Python (Google Colab).
Tahapan meliputi:
- Pemeriksaan kualitas data
- Analisis korelasi
- Statistik deskriptif
- Clustering (K-Means)
- Klasifikasi (KNN)

## 1. Import Library

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.datasets import load_iris
from sklearn.cluster import KMeans
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

## 2. Load Dataset Iris

iris = load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
df['species'] = iris.target
df.head()

## 3. Pemeriksaan Kualitas Data

print("Missing Values:")
print(df.isnull().sum())

print("\nJumlah Data Duplikat:")
print(df.duplicated().sum())

## 4. Statistik Deskriptif
df.describe()
### Histogram Distribusi Fitur

df.iloc[:, :4].hist()
plt.show()

## 5. Analisis Korelasi

corr = df.iloc[:, :4].corr()
corr


plt.figure()
sns.heatmap(corr, annot=True)
plt.title("Correlation Matrix Iris Dataset")
plt.show()

## 6. Clustering Menggunakan K-Means

kmeans = KMeans(n_clusters=3, random_state=42)
df['cluster'] = kmeans.fit_predict(df.iloc[:, :4])
df[['species','cluster']].head()

## 7. Klasifikasi Menggunakan KNN

X = df.iloc[:, :4]
y = df['species']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)

model = KNeighborsClassifier(n_neighbors=3)
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

print("Accuracy:", accuracy_score(y_test, y_pred))


print("Confusion Matrix:")
print(confusion_matrix(y_test, y_pred))

print("\nClassification Report:")
print(classification_report(y_test, y_pred))
