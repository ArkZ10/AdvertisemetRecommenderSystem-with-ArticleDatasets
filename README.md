# Laporan Proyek Rekomendasi Sistem - Yeftha Joshua Ezekiel

## Project Overview

Kemajuan teknologi pembelajaran mesin telah memungkinkan model seperti content-based filtering dan collaborative filtering menjadi alat yang sangat efektif dalam merekomendasikan iklan kepada pengguna. Model ini mampu menganalisis data dalam skala besar dengan akurasi tinggi, menghasilkan wawasan yang mendalam tentang preferensi dan perilaku pengguna. Dengan memanfaatkan data seperti kategori konten yang disukai atau pola kesamaan antara pengguna, teknologi ini dapat menyajikan rekomendasi yang lebih relevan, personal, dan sesuai dengan kebutuhan setiap individu, sehingga meningkatkan pengalaman pengguna sekaligus efektivitas pemasaran.

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

SUMBER DATA:

[Advertisement - Click on Ad dataset](https://www.kaggle.com/datasets/gabrielsantello/advertisement-click-on-ad).

[News Article Category Dataset](https://www.kaggle.com/datasets/timilsinabimal/newsarticlecategories)

Variabel-variabel dalam dataset
1. Dataset Iklan (`(6877, 3)`)
   - articleId: ID unik untuk setiap artikel.
   - category: Kategori artikel.
     - ARTS AND CULTURE: 1002
     - BUSINESS: 501
     - COMEDY: 380
     - CRIME: 300
     - EDUCATION: 490
     - ENTERTAINMENT: 501
     - ENVIRONMENT: 501
     - MEDIA: 347
     - POLITICS: 501
     - RELIGION: 501
     - SCIENCE: 350
     - SPORTS: 501
     - TECH: 501
     - WOMEN: 501
   - title: Judul artikel yang menggambarkan konten iklan.

2. Dataset Pengguna (`(1000,10)`)
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
  
3. Kondisi Data
   Data yang diambil pada opensource kaggle tidak ada missing value, duplikat, ataupun outlier. 

![image](https://github.com/user-attachments/assets/2bb8826a-531e-4a01-b565-c3154a50c4ef)

Dataset articlesDF memiliki 6,877 entri dengan 3 kolom (category, title, dan body), di mana kolom body memiliki 1 nilai kosong yang perlu ditangani, sementara kolom lainnya lengkap dan siap digunakan. Dataset ini menggunakan memori sebesar 161.3 KB, dan jika ada ketidakseimbangan jumlah artikel antar kategori, normalisasi data dapat diterapkan. Dataset usersDF berisi 1,000 entri dengan 10 kolom, di mana beberapa kolom seperti Ad Topic Line, City, Country, dan Timestamp kemungkinan tidak relevan untuk sistem rekomendasi sehingga dapat dihapus, sementara kolom numerik seperti Daily Time Spent on Site, Age, dan Area Income dapat dinormalisasi untuk meningkatkan performa model. Dengan semua kolom lengkap tanpa nilai kosong dan ukuran dataset yang kecil (78.2 KB), kedua dataset cukup ringan dan siap diproses setelah dilakukan pembersihan dan normalisasi.

     
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

4. Membuat Matriks Interaksi Kategori Pengguna
   - Gabungan Data

     Data interaksi pengguna-artikel (user_article_df) digabungkan dengan dataset artikel (articlesDF) berdasarkan kolom articleId.

     `interactions_df = user_article_df.merge(articlesDF, on='articleId')`
   - Grup dan Unstack

     Matriks interaksi dibuat menggunakan teknik pengelompokan berdasarkan userId dan kategori artikel (category):
     Setiap sel pada matriks berisi jumlah artikel yang diakses pengguna dalam kategori tertentu. Matriks diisi dengan 0 jika tidak ada interaksi pada kategori tersebut.
   
     `user_category_matrix = interactions_df.groupby(["userId", "category"]).size().unstack(fill_value=0)`



## Modeling
### Content-Based Filtering

#### Cara Kerja Content-Based Filtering
Model ini memprediksi apakah seorang pengguna akan berinteraksi dengan kategori tertentu (output biner: 0 atau 1). Model menggunakan dua input utama:
1. **Preferensi Pengguna (X_user)**: Representasi preferensi pengguna terhadap berbagai kategori artikel, yang didapatkan dari data historis interaksi.
2. **Vektor Kategori (X_category)**: One-hot encoding yang menunjukkan kategori artikel tertentu.

Dengan menggabungkan kedua input tersebut melalui **layer Concatenate**, model belajar memahami hubungan antara preferensi pengguna dan kategori artikel untuk memprediksi interaksi.

#### Detail Arsitektur Model dan Parameternya
**1. Input Layers**
- **`user_input`**: Vektor panjang `num_categories`, berisi nilai yang mewakili preferensi pengguna terhadap setiap kategori.
- **`category_input`**: Vektor panjang `num_categories`, berupa one-hot encoding dari kategori artikel.
- **Parameter**: Panjang input (`shape=(num_categories,)`) didasarkan pada jumlah kategori dalam dataset.
- **`X_user`**: Dibangun dari `user_category_matrix`, yang memuat informasi historis preferensi pengguna terhadap berbagai kategori. Jika data pengguna tidak tersedia, input diisi dengan nol.
- **`X_category`**: Vektor one-hot encoding untuk setiap kategori, menunjukkan kategori spesifik yang sedang diproses.
- **`y`**: Target output berupa **1** jika pengguna berinteraksi dengan kategori (berdasarkan `interactions_df`) dan **0** jika tidak.

**2. Concatenate Layer**
- Menggabungkan kedua input (`user_input` dan `category_input`) menjadi satu vektor panjang `2 * num_categories`. 
- **Tujuan**: Memberikan model informasi terintegrasi tentang pengguna dan kategori yang sedang diproses.

**3. Hidden Layers**
- **`Dense(64, activation='relu')`**:
  - Lapisan pertama dengan 64 neuron dan fungsi aktivasi **ReLU** (Rectified Linear Unit).
  - **Fungsi**: Mengekstraksi hubungan non-linear antara preferensi pengguna dan kategori.
- **`Dense(32, activation='relu')`**:
  - Lapisan kedua dengan 32 neuron.
  - **Fungsi**: Mengurangi dimensi data dan menyaring informasi untuk mendekati keputusan akhir.

**4. Output Layer**
- **`Dense(1, activation='sigmoid')`**:
  - Lapisan terakhir dengan 1 neuron dan fungsi aktivasi sigmoid.
  - **Fungsi**: Menghasilkan probabilitas (antara 0 dan 1) yang menunjukkan kemungkinan interaksi pengguna dengan kategori tertentu.

**5. Model Compilation**
- **Optimizer**: `adam`
  - Algoritma optimasi adaptif yang efisien untuk memperbarui bobot berdasarkan gradien error.
- **Loss Function**: `binary_crossentropy`
  - Fungsi loss untuk klasifikasi biner, menghitung perbedaan antara prediksi dan label aktual.
- **Metric**: `accuracy`
  - Metrik evaluasi untuk melacak akurasi selama pelatihan.


Hasil Top N Recommendations:
- Article: Anderson Cooper Shreds Trump: ‘He Went To Play Golf While They Held Funerals’ (ID: article_2101, PROB: 0.57)
- Article: How Many Times Can Wolf Blitzer Avoid Saying 'Shithole'? (ID: article_2102, PROB: 0.57)
- Article: Parents Of Slain DNC Staffer Seth Rich Sue Fox News Over Fake News Story (ID: article_2103, PROB: 0.57)
- Article: Media Euphemisms For 'Racist' Are Stupidly Tinged (ID: article_2104, PROB: 0.57)
- Article: Ted Cruz Makes It Too Easy To Point Out The Hypocrisy Of His Latest Campaign Ad (ID: article_2105, PROB: 0.57)




### Collaborative Filtering

#### **Cara Kerja Collaborative Filtering**
Model ini memprediksi apakah seorang pengguna akan berinteraksi dengan sebuah artikel berdasarkan:
1. **Embeddings**:
   - Menggunakan embedding untuk mewakili pengguna dan artikel dalam ruang vektor berdimensi rendah, sehingga dapat menangkap pola hubungan yang kompleks.
2. **Fitur Tambahan**:
   - Fitur tambahan dari pengguna seperti **usia**, **pendapatan**, dan **waktu yang dihabiskan di situs** digunakan untuk memperkaya representasi pengguna.

Model ini menggunakan tiga input utama:
1. **ID pengguna (`user_id`)**
2. **ID artikel (`article_id`)**
3. **Fitur tambahan pengguna (`user_features`)**


#### **Detail Arsitektur Model dan Parameternya**

**1. Normalisasi Data**
- **`MinMaxScaler`**:
  - Fitur tambahan pengguna (`Daily Time Spent on Site`, `Age`, `Area Income`) dinormalisasi ke rentang [0, 1].
  - **Tujuan**: Meningkatkan stabilitas pelatihan model dan mempercepat konvergensi.

**2. Representasi Data**
- **Artikel**:
  - Setiap artikel diberikan **indeks unik** menggunakan `article_to_idx`.
- **Interaksi**:
  - Dibangun matriks interaksi biner (`interactions_matrix`), di mana nilai **1** menunjukkan adanya interaksi antara pengguna dan artikel.

**3. Embedding Layers**
- **User Embedding (`user_embedding`)**:
  - Dimensi input: `num_users`
  - Dimensi output: `embedding_dim=50`
  - **Fungsi**: Mengonversi ID pengguna ke representasi vektor berdimensi rendah.
- **Article Embedding (`article_embedding`)**:
  - Dimensi input: `num_articles`
  - Dimensi output: `embedding_dim=50`
  - **Fungsi**: Mengonversi ID artikel ke representasi vektor berdimensi rendah.
- **Flatten**:
  - Embedding diratakan agar dapat digabungkan dengan input lain.

**4. Fitur Tambahan**
- **`user_features`**:
  - Fitur tambahan pengguna: **usia, pendapatan, waktu di situs**.
  - Langsung digabungkan dengan embedding pengguna dan artikel menggunakan layer **Concatenate**.

**5. Hidden Layers**
- **Dense Layer (32 Neurons)**:
  - Aktivasi: **ReLU**
  - **Fungsi**: Mengekstraksi hubungan non-linear antara embedding pengguna, embedding artikel, dan fitur tambahan.
- **Dense Layer (16 Neurons)**:
  - Aktivasi: **ReLU**
  - **Fungsi**: Menyaring informasi sebelum ke layer output.

**6. Output Layer**
- **Dense (1 Neuron)**:
  - Aktivasi: **Sigmoid**
  - **Fungsi**: Menghasilkan probabilitas interaksi (nilai antara 0 dan 1).

**7. Model Compilation**
- **Optimizer**: `adam`
  - Digunakan untuk mengoptimalkan bobot model dengan adaptasi pembelajaran.
- **Loss Function**: `binary_crossentropy`
  - Mengukur kesalahan prediksi pada klasifikasi biner.
- **Metric**: `accuracy`
  - Digunakan untuk memantau kinerja model selama pelatihan.


Hasil Top N Recommendations:
- Article ID: article_1889, Title: UN Climate Talks May Only Bring Moderate Progress As Rich Nations Worry About Economy
- Article ID: article_2306, Title: Tucker Carlson Turns On Trump: 'Imagine If Barack Obama Had Said That'
- Article ID: article_2888, Title: When Patriotism Becomes Idolatry
- Article ID: article_1049, Title: Cops Explain How To Pull Off A Good Halloween Prank Without Getting Arrested
- Article ID: article_815, Title: 'Late Night' Writer's Breathless Royal Wedding Recap Is The Only One You Need



### Kelebihan dan kekurangan kedua model
   
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
\text{Accuracy} = \frac{\text{Jumlah Prediksi Benar}}{\text{Total Data}}
$$

#### Loss

Mengukur seberapa jauh prediksi model dari nilai target sebenarnya. Untuk klasifikasi biner, biasanya digunakan binary crossentropy. Memandu model untuk mengurangi kesalahan dalam prediksi. Semakin kecil nilainya, semakin baik modelnya dalam menyesuaikan data.

$$
\text{Loss} = -\frac{1}{N} \sum_{i=1}^N \left( y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right)
$$

