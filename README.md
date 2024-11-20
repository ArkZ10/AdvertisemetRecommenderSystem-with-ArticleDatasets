# Laporan Proyek Rekomendasi Sistem - Yeftha Joshua Ezekiel

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
1. Content-Based Filtering
   
   Model yang pertama ini membangun sistem rekomendasi berbasis content-based filtering menggunakan model deep learning untuk memprediksi minat pengguna terhadap iklan.
   - Membangun Model:
     
     Input dari preferensi pengguna (user_input) dan kategori artikel (category_input) digabungkan. Lapisan dense dengan aktivasi ReLU memproses data, menghasilkan output probabilitas interaksi.
   - Persiapan Data:

     Vektor preferensi pengguna diambil dari matriks kategori. Kategori artikel direpresentasikan dalam bentuk satu-hot encoding. Label target (y) ditentukan berdasarkan ada/tidaknya interaksi pengguna dengan kategori.
   - Pelatihan Model:

     Model dilatih untuk memprediksi apakah pengguna tertarik pada kategori tertentu.
   - Prediksi dan Rekomendasi:

     Vektor preferensi pengguna baru dibangun berdasarkan artikel yang pernah mereka baca. Artikel yang relevan dievaluasi menggunakan model, dan rekomendasi diurutkan berdasarkan probabilitas tertinggi. Sistem ini menghasilkan daftar rekomendasi personal berdasarkan kesamaan konten iklan dan preferensi pengguna.

2. Collaborative Filtering

   Model yang kedua ini membangun sistem rekomendasi berbasis collaborative filtering menggunakan model deep learning untuk memprediksi minat pengguna terhadap iklan.
   - Membangun Model:
     - Input: Fitur pengguna seperti Age, Income, dan Time Spent dimasukkan sebagai input numerik. ID pengguna dan ID artikel dimasukkan ke dalam embedding layer untuk menghasilkan representasi vektor dari kedua entitas.
     - Embedding Layer: Mengubah ID artikel dan ID user menjadi vektor yang berdimensi rendah.
     - Dense Layer: Data yang telah digabungkan diproses melalui beberapa lapisan Dense dengan aktivasi ReLU untuk mengekstraksi fitur lebih lanjut.
     - Output Layer: Lapisan akhir menggunakan sigmoid activation untuk menghasilkan probabilitas apakah pengguna akan berinteraksi dengan artikel tertentu (0 atau 1).

   - Pelatihan Model:
     - Model dilatih menggunakan binary cross-entropy loss untuk memprediksi apakah pengguna tertarik pada artikel tertentu. Optimasi dilakukan dengan Adam optimizer.
     - Input Training: ID pengguna, ID artikel, dan fitur pengguna disiapkan sebagai input untuk model.

   - Prediksi dan Rekomendasi:
     - Normalisasi Fitur Pengguna Baru: Fitur pengguna baru dinormalisasi menggunakan scaler yang sama agar dapat diproses dalam model.
     - Prediksi Probabilitas: Model digunakan untuk memprediksi probabilitas bahwa pengguna baru tertarik pada setiap artikel.
     - Pengecualian Artikel yang Sudah Dilihat: Artikel yang sudah pernah dilihat oleh pengguna (berdasarkan input interacted_articles) dikeluarkan dari daftar rekomendasi.
     - Pengurutan dan Pemilihan Rekomendasi: Artikel yang memiliki probabilitas tertinggi dipilih sebagai rekomendasi teratas.

3. Kelebihan dan kekurangan kedua model
   
| Aspek                        | Content-Based Filtering                     | Collaborative Filtering                   |
|------------------------------|---------------------------------------------|-------------------------------------------|
| **Cold-Start**               | Baik untuk artikel baru                    | Sulit tanpa interaksi                     |
| **Eksplorasi Artikel Baru**  | Cenderung merekomendasikan konten serupa    | Lebih beragam karena memanfaatkan pola    |
| **Bergantung pada Fitur**    | Sangat bergantung                          | Tidak bergantung                          |
| **Data Interaksi**           | Tidak digunakan                            | Sangat penting                           |
| **Kompleksitas Model**       | Lebih sederhana                            | Lebih kompleks                            |


## Evaluation

Metrik Evaluasi: accuracy dan loss, yang diukur selama proses pelatihan.

Accuracy mengukur persentase prediksi yang benar dibandingkan dengan data sebenarnya, mencerminkan efektivitas model dalam membuat rekomendasi yang relevan.
Loss menunjukkan kesalahan total model selama pelatihan, di mana nilai yang lebih kecil menunjukkan model yang lebih baik dalam mempelajari data.

Metrik ini dipilih karena sesuai dengan konteks proyek:
- Problem Statement: Metrik ini membantu menentukan apakah rekomendasi yang diberikan relevan dengan preferensi pengguna.
- Solusi yang Diinginkan: Tingginya nilai akurasi dan rendahnya nilai loss mencerminkan kemampuan model dalam merekomendasikan iklan yang relevan.

**Model Content-Based Filtering**
| Epoch | Accuracy | Loss   |
|-------|----------|--------|
| 1     | 86.62%   | 0.3749 |
| 2     | 89.69%   | 0.3197 |
| 3     | 89.19%   | 0.3155 |
| 4     | 89.06%   | 0.3055 |
| 5     | 89.71%   | 0.2675 |

- Model berhasil mencapai akurasi 89.71% pada akhir pelatihan, menunjukkan kinerja yang stabil untuk merekomendasikan iklan berbasis preferensi pengguna.
- Nilai loss yang terus menurun hingga 0.2675 mengindikasikan bahwa model belajar dengan baik dari data, dan prediksinya semakin akurat.

**Model Collaborative Filtering**
| Epoch | Accuracy | Loss   |
|-------|----------|--------|
| 1     | 49.35%   | 0.6941 |
| 2     | 55.88%   | 0.6851 |
| 3     | 63.87%   | 0.6389 |
| 4     | 71.16%   | 0.5644 |
| 5     | 77.99%   | 0.4701 |

- Model collaborative filtering menunjukkan peningkatan akurasi yang signifikan dari 49.35% (Epoch 1) menjadi 77.99% (Epoch 5).
- Nilai loss yang menurun hingga 0.4701 mencerminkan kemampuan model untuk menangkap pola interaksi antara pengguna dan artikel dengan lebih baik selama pelatihan.

#### Accuracy

Mengukur persentase prediksi yang benar dari total data. Memberikan gambaran seberapa baik model membuat prediksi yang benar secara keseluruhan. Semakin tinggi, semakin baik performanya.

$$
\[
\text{Accuracy} = \frac{\text{Jumlah Prediksi Benar}}{\text{Total Data}}
\]
$$

#### Loss

Mengukur seberapa jauh prediksi model dari nilai target sebenarnya. Untuk klasifikasi biner, biasanya digunakan binary crossentropy. Memandu model untuk mengurangi kesalahan dalam prediksi. Semakin kecil nilainya, semakin baik modelnya dalam menyesuaikan data.

$$
\[
\text{Loss} = -\frac{1}{N} \sum_{i=1}^N \left( y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right)
\]
$$

