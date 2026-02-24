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