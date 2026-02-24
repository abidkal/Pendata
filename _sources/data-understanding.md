
# Eksplorasi Dataset Iris
## Data Understanding dan Analisis

Notebook ini berisi proses eksplorasi dataset Iris secara bertahap,
mulai dari pemeriksaan kualitas data hingga percobaan pemodelan sederhana.

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

## 2. Load Dataset

iris = load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
df['species'] = iris.target
df.head()


Dataset terdiri dari 150 baris data dengan empat fitur numerik.
Kolom species merupakan label kelas.

## 3. Pemeriksaan Kualitas Data

print("Missing Values:")
print(df.isnull().sum())

print("\nData Duplikat:")
print(df.duplicated().sum())

## 4. Statistik Deskriptif
df.describe()
### Histogram Distribusi Fitur

df.iloc[:, :4].hist(figsize=(8,6))
plt.tight_layout()
plt.show()

## 5. Analisis Korelasi

corr = df.iloc[:, :4].corr()
corr


plt.figure(figsize=(6,4))
sns.heatmap(corr, annot=True)
plt.title("Matriks Korelasi Iris")
plt.show()


Korelasi tertinggi terlihat pada petal length dan petal width.

## 6. Clustering (K-Means)

kmeans = KMeans(n_clusters=3, random_state=42)
df['cluster'] = kmeans.fit_predict(df.iloc[:, :4])

df[['species','cluster']].head()

## 7. Klasifikasi (KNN)

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
