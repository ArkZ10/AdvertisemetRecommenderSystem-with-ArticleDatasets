## Project Overview

Kemajuan teknologi pembelajaran mesin telah memungkinkan model seperti content-based filtering dan collaborative filtering menjadi alat yang sangat efektif dalam merekomendasikan iklan kepada pengguna. Model ini mampu menganalisis data dalam skala besar dengan akurasi tinggi, menghasilkan wawasan yang mendalam tentang preferensi dan perilaku pengguna. Dengan memanfaatkan data seperti kategori konten yang disukai atau pola kesamaan antara pengguna, teknologi ini dapat menyajikan rekomendasi yang lebih relevan, personal, dan sesuai dengan kebutuhan setiap individu, sehingga meningkatkan pengalaman pengguna sekaligus efektivitas pemasaran.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Proyek ini penting untuk diselesaikan karena sistem rekomendasi iklan yang efektif dapat memberikan nilai tambah yang signifikan bagi pengguna dan bisnis. Bagi pengguna, rekomendasi yang relevan membantu menemukan informasi atau produk yang sesuai dengan kebutuhan mereka tanpa perlu mencarinya secara manual, sehingga meningkatkan pengalaman yang lebih personal dan efisien. Bagi bisnis, sistem ini dapat meningkatkan konversi dan keterlibatan pengguna, mengoptimalkan strategi pemasaran, dan memaksimalkan pendapatan. Dengan menggunakan pendekatan seperti content-based filtering dan collaborative filtering, proyek ini juga menjadi langkah nyata dalam pemanfaatan data secara cerdas untuk mengungkap pola perilaku pengguna yang tidak terlihat secara langsung. Di era digital dengan informasi yang melimpah, keberadaan sistem rekomendasi menjadi solusi penting untuk mengatasi tantangan kelebihan informasi dan memastikan iklan yang ditampilkan tepat sasaran.

Format Referensi:
- [Konapure, R. C., & Lobo, L. M. R. J. (2021). Video content-based advertisement recommendation system using classification technique of machine learning. *Journal of Physics: Conference Series, 1854*(1), 012025.](https://doi.org/10.1088/1742-6596/1854/1/012025)

- [Michael D. Ekstrand, John T. Riedl and Joseph A. Konstan (2011), "Collaborative Filtering Recommender Systems", Foundations and Trends® in Human–Computer Interaction: Vol. 4: No. 2, pp 81-173.](http://dx.doi.org/10.1561/1100000009).

## Business Understanding

Penjelasan proses klarifikasi masalah

### Problem Statements

- Bagaimana merekomendasikan iklan yang relevan kepada pengguna dengan mempertimbangkan preferensi mereka?
- Bagaimana memberikan rekomendasi awal yang efektif untuk pengguna baru tanpa data historis?
- Bagaimana menyaring informasi yang berlebihan agar hanya iklan yang relevan yang ditampilkan kepada pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Mengembangkan sistem rekomendasi iklan yang dapat menampilkan konten yang relevan dan menarik bagi pengguna berdasarkan preferensi mereka.
- Menyediakan rekomendasi yang efektif untuk pengguna baru meskipun tidak ada data klik sebelumnya.
- Meningkatkan pengalaman pengguna dengan menyaring iklan agar lebih relevan dan mengurangi kelebihan informasi.

**Rubrik/Kriteria Tambahan (Opsional)**:

### Solution statements

1. Content-Based Filtering:
Menggunakan kategori artikel atau iklan yang sebelumnya diakses oleh pengguna untuk merekomendasikan konten dari kategori serupa. Misalnya, jika pengguna membaca artikel tentang "Teknologi", sistem akan merekomendasikan artikel lain dalam kategori "Teknologi" atau kategori yang terkait.

2. Collaborative Filtering:

- User-Based Collaborative Filtering:
Mencari pengguna dengan profil serupa berdasarkan atribut seperti usia, pendapatan, dan waktu yang dihabiskan di platform. Sistem kemudian merekomendasikan iklan yang telah diklik oleh pengguna serupa.

- Item-Based Collaborative Filtering:
Mengidentifikasi kesamaan antara iklan berdasarkan pola klik pengguna. Jika pengguna A dan pengguna B memiliki preferensi yang mirip, sistem akan merekomendasikan iklan yang belum dilihat tetapi relevan dengan klik sebelumnya.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
