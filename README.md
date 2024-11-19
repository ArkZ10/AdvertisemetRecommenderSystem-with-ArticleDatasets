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
Dataset yang digunakan dalam proyek ini mencakup data iklan dan data pengguna. Dataset iklan yang dipakai merupakan data artikel yang juga mengsimulasikan iklan, termasuk kategori, judul, dan ID unik setiap artikel. Dataset pengguna mencakup atribut demografi dan perilaku pengguna, seperti usia, pendapatan, dan waktu harian yang dihabiskan di situs. Terdapat data dummy juga yang dibuat untuk mengsimulasikan iklan yang di klik oleh pengguna. Dataset iklan terdiri dari 14 kategori, masing-masing memiliki 300 artikel yang sudah dinormalisasi. Dataset pengguna mencakup 1.000 pengguna yang secara acak memilih 4 artikel sebagai klik mereka.

[Advertisement - Click on Ad dataset](https://www.kaggle.com/datasets/gabrielsantello/advertisement-click-on-ad).

[News Article Category Dataset](https://www.kaggle.com/datasets/timilsinabimal/newsarticlecategories)

Variabel-variabel dalam dataset
1. Dataset Iklan
   - articleId: ID unik untuk setiap artikel.
   - category: Kategori artikel. 
   - title: Judul artikel yang menggambarkan konten iklan.

2. Dataset Pengguna
   - 'Daily Time Spent on Site': consumer time on site in minutes
   - 'Age': customer age in years
   - 'Area Income': Avg. Income of geographical area of consumer
   - 'Daily Internet Usage': Avg. minutes a day consumer is on the internet
   - 'Ad Topic Line': Headline of the advertisement
   - 'City': City of consumer
   - 'Male': Whether or not consumer was male
   - 'Country': Country of consumer
   - 'Timestamp': Time at which consumer clicked on Ad or closed window
   - 'Clicked on Ad': 0 or 1 indicated clicking on Ad

**Rubrik/Kriteria Tambahan (Opsional)**:
![image](https://github.com/user-attachments/assets/2bb8826a-531e-4a01-b565-c3154a50c4ef)

Dengan melakukan ini, kita dapat memahami kondisi awal dataset, menentukan langkah-langkah preprocessing yang diperlukan (seperti menghapus kolom tidak relevan atau menangani nilai kosong), serta memastikan bahwa data siap untuk digunakan dalam analisis.

     
## Data Preparation
1. Dataset Artikel (**articlesDF**)
   - Pembersihan Data
     Dataset awal artikel berisi informasi tentang judul artikel, kategori, isi artikel (body), dan atribut lainnya. Kolom body dihapus karena tidak relevan untuk sistem rekomendasi yang lebih berfokus pada kategori dan judul artikel.

      `articlesDF = articlesDF.drop(columns=['body'], axis=1)`
   - Distribusi Kategori Data
     Analisis awal menunjukkan bahwa jumlah artikel per kategori bervariasi. Untuk memastikan keseimbangan dalam sistem rekomendasi, setiap kategori dibatasi hingga 300 artikel menggunakan teknik normalisasi. Hasil normalisasi memastikan bahwa dataset memiliki jumlah artikel yang merata dari setiap kategori.

     `articlesDF = articlesDF.groupby('category', group_keys=False).apply(lambda x: x.sample(min(len(x), 300)))`
   - Penambahan ID
     Setiap artikel diberikan ID unik dalam format article_X, di mana X adalah angka urut. Hal ini mempermudah proses pelacakan artikel.

     `articlesDF['articleId'] = ['article_' + str(i) for i in range(1, len(articlesDF) + 1)]`

2. Dataset Pengguna (**usersDF**)
   - Pembersihan Data
     Dataset pengguna berisi berbagai atribut, seperti waktu yang dihabiskan di internet, topik iklan, lokasi geografis, dan lainnya. Kolom Daily Internet Usage, Ad Topic Line, City, Male, Country, Timestamp, dan Clicked on Ad dihapus karena tidak relevan dengan sistem rekomendasi.

     `usersDF = usersDF.drop(columns=['Daily Internet Usage', 'Ad Topic Line', 'City', 'Male', 'Country', 'Timestamp', 'Clicked on Ad'], axis=1)`
   - Penambahan ID
     Setiap pengguna diberikan ID unik dalam format angka untuk mempermudah identifikasi pengguna.

     `usersDF['userId'] = [i for i in range(1, len(usersDF) + 1)]`

3. Data Dummy: Interaksi Pengguna dengan Artikel (iklan) (**user_article_df**)
   - Pembuatan Data Dummy
     Untuk mensimulasikan interaksi antara pengguna dan artikel, setiap pengguna secara acak memilih 4 artikel dari dataset artikel. Data ini disusun dalam format pasangan userId dan articleId

     ```
     dummy_data = []
     for user in usersDF["userId"]:
         chosen_articles = np.random.choice(articlesDF["articleId"], 4, replace=False)
         for article in chosen_articles:
             dummy_data.append({"userId": user, "articleId": article})
             user_article_df = pd.DataFrame(dummy_data)
     ```

   - Validasi Data Dummy
     Validasi dilakukan untuk memastikan tidak ada kombinasi user-article yang duplikat. Hasil validasi menunjukkan bahwa setiap kombinasi unik, sehingga data siap digunakan.

     ```
     unique_counts = user_article_df.value_counts().unique()
     if len(unique_counts) == 1 and unique_counts[0] == 1:
         print("Validation passed: No duplicate user-article combinations.")
     ```


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
