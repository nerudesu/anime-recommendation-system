# Laporan Proyek Machine Learning - Pradipta A. Suryadi

## Project Overview
Industri anime telah mengalami pertumbuhan yang signifikan dan peningkatan popularitas secara global, menciptakan pasar yang berkembang pesat untuk bisnis terkait anime ([AJA, 2023](https://aja.gr.jp/english/japan-anime-data))[^1]. Sistem rekomendasi anime memainkan peran penting dalam industri anime dengan membantu *user* menemukan judul anime baru dan meningkatkan pengalaman menonton mereka. Beberapa latar belakang tentang aspek bisnis dari sistem rekomendasi anime, sebagai berikut:

1.  **Permintaan pasar**
    Permintaan akan konten anime terus meningkat di seluruh dunia. Penggemar anime terus mencari judul baru yang menarik untuk ditonton. Namun, banyaknya serial anime yang tersedia dapat membuat *user* kewalahan untuk menemukan konten yang sesuai dengan preferensi mereka. Sistem rekomendasi anime mengatasi tantangan ini dengan memberikan rekomendasi yang dipersonalisasi. Tidak hanya meningkatkan kepuasan pengguna tetapi juga mendorong interaksi dan retensi.

2.  **Keterlibatan dan Retensi *User***
    Dengan menawarkan rekomendasi yang dipersonalisasi, sistem rekomendasi anime dapat secara signifikan meningkatkan keterlibatan *user* dan tingkat retensi. *User* cenderung menghabiskan lebih banyak waktu di platform atau layanan yang memahami preferensi mereka dan secara konsisten menyarankan judul anime yang relevan. Keterlibatan dan retensi *user* yang ditingkatkan berkontribusi pada peningkatan loyalitas, rekomendasi dari mulut ke mulut, dan potensi pertumbuhan pendapatan.

3.  **Penemuan Konten**
    Sistem rekomendasi anime memungkinkan *user* menemukan judul anime baru dan kurang dikenal yang sesuai dengan minat mereka. Ini tidak hanya menguntungkan *user* dengan memperluas khazanah anime mereka, tetapi juga mendukung pembuat konten dan studio produksi. Hal ini memungkinkan promosi serial anime yang *niche* dan beragam, yang mungkin memiliki keterpaparan terbatas dibandingkan dengan judul *mainstream*. Dengan memfasilitasi penemuan konten, sistem rekomendasi anime berkontribusi pada industri anime yang lebih beragam dan dinamis.

4.  **Penghasilan Pendapatan**
    Sistem rekomendasi anime dapat dimonetisasi dengan berbagai cara. Beberapa potensi pendapatan:
    -   Periklanan
        Sistem rekomendasi dapat menampilkan iklan bertarget berdasarkan preferensi pengguna dan kebiasaan menonton, menghasilkan pendapatan iklan.
    -   Langganan Premium
        Menawarkan langganan premium dengan fitur tambahan akses awal ke anime yang direkomendasikan.
    -   Merchandising dan Affiliate Marketing
        Bermitra dengan produsen merchandise, pengecer, atau platform pemasaran terafiliasi untuk mempromosikan dan menjual produk terkait anime.
    -   Kemitraan Lisensi dan Distribusi
        Berkolaborasi dengan platform streaming atau *broadcaster* untuk memperluas jangkauan dan distribusi judul anime yang direkomendasikan.

5.  **Data *User* dan Analitik**
    Sistem rekomendasi anime menghasilkan data dan analitik *user* yang berharga, memberikan pengetahuan tentang preferensi pengguna, kebiasaan menonton, dan tren. Data ini dapat digunakan untuk riset pasar, perencanaan konten, dan strategi pemasaran bertarget. Menganalisis perilaku dan preferensi pengguna dapat membantu bisnis memahami audiens target mereka dengan lebih baik, mengembangkan kampanye pemasaran bertarget, dan meningkatkan keputusan akuisisi konten.

6.  **Keunggulan kompetitif**
    Menerapkan sistem rekomendasi anime yang kuat dan akurat dapat memberikan keuntungan kompetitif bagi bisnis di industri anime. Sistem rekomendasi yang unggul dapat menarik dan mempertahankan *user*, membedakan platform atau layanan dari pesaing, dan membangun reputasi untuk memberikan rekomendasi hasil personalisasi berkualitas tinggi. Bisnis dapat mempertahankan keunggulan kompetitif di pasar dengan terus meningkatkan algoritma rekomendasi dan tetap up-to-date dengan penelitian terbaru dan tren industri.

Pengembangan sistem rekomendasi anime cukup banyak dilakukan oleh para peneliti, misalnya pengembangan sistem rekomendasi anime yang menggabungkan teknik collaborative filtering dan content-based filtering ([Mugeswari, R., 2019](https://ijcsis.org/papers/vol17no4/A-2637.pdf))[^2]. Penelitian ini mengeksplorasi tantangan dalam merekomendasikan judul anime dan mengusulkan pendekatan hybrid untuk mengatasinya. Studi ini mencakup penjelasan rinci tentang arsitektur sistem rekomendasi, preprocessing data, dan algoritma yang digunakan untuk penyaringan kolaboratif dan penyaringan berbasis konten. Penelitian ini juga menyajikan hasil eksperimen dan evaluasi untuk menilai kinerja dan efektivitas sistem yang diusulkan.

## Business Understanding
Sistem rekomendasi anime memiliki implikasi bisnis yang signifikan bagi industri anime. Dengan memanfaatkan data dan analitik pengguna, bisnis dapat lebih memahami audiens mereka dan memberikan rekomendasi yang dipersonalisasi yang meningkatkan pengalaman pengguna secara keseluruhan dan mendorong pertumbuhan bisnis.

### Problem Statements
Berdasarkan uraian sebelumnya, rumusan masalah dalam proyek ini adalah:
- Berdasarkan data yang tersedia, bagaimana membuat sistem rekomendasi dengan teknik *content-based filtering*?
- Dengan data rating dari *user*, bagaimana perusahaan dapat merekomendasikan anime lain yang mungkin disukai dan belum pernah ditonton *user*?

### Goals
Tujuan yang ingin dicapai dari proyek ini adalah:
- Menghasilkan sistem rekomendasi anime berdasarkan kemiripan *features*-nya.
- Menghasilkan sistem rekomendasi anime berdasarkan kemiripan penilaian *user* terhadap *anime* yang sudah pernah ditonton sebelumnya.

### Solution approach
Solusi yang diajukan untuk menyelesaikan permasalahan adalah:
1. Membuat sistem rekomendasi dengan teknik **Content-based Filtering (CBF)** berdasarkan *features* anime.
2. Membuat sistem rekomendasi dengan teknik **Collaborative Filtering (CF)** berdasarkan rating dari *user*.

## Data Understanding
Kita akan menggunakan dataset [Anime Recomendation System](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)[^3] yang tersedia di Kaggle. Data ini didownload ke workspace Google Collaboratory menggunakan API Kaggle.

Variabel-variabel pada Anime Recommendation System dataset adalah sebagai berikut:
Anime.csv
* anime_id - ID unik myanimelist.net yang mengidentifikasi anime.
* name - Nama lengkap anime
* genre - Daftar genre yang dipisahkan koma untuk anime ini.
* type - movie, TV, OVA, etc.
* episodes - Jumlah episode dalam anime ini. (1 jika type adalah movie).
* rating - Rating rata-rata (skala 1 sampai 10) untuk anime ini.
* members - Jumlah anggota komunitas yang tergabung dalam "grup" anime ini.

Rating.csv
* user_id - ID user yang dihasilkan secara acak sehingga tidak dapat diidentifikasi.
* anime_id - Anime yang telah diberi peringkat oleh user ini.
* rating - Peringkat (skala 1 sampai 10) yang diberikan pengguna ini (-1 jika user menontonnya tetapi tidak memberikan peringkat).

Pada tahapan ini dilakukan Exploratory Data Analysis (EDA) untuk mendapatkan pemahaman pada data.
1.  Anime Dataset
    Pada Anime Dataset terdapat 12.294 baris dan 7 kolom, dengan rincian:
    -  3 kolom numerikal (anime_id, rating, members)
    -  4 kolom kategorikal (name, genre, type, episodes)

    Dilakukan juga Data Cleansing, seperti:
    1. Pada kolom episodes dan merubah tipe datanya dari kategorikal menjadi numerikal.
    2. Mengecek duplikasi dan membuang nilai Null
    
    Kita juga melakukan analisis statistik pada data numerik dan didapatkan informasi:
    1. Jumlah episode paling sedikit adalah satu, sesuai deskripsi dataset angka 1 bisa saja anime bertipe Movie. Jumlah episode terbanyak adalah 1818.
    2. Rating anime terendah ada di angka 1.67 dan rating tertingginya adalah nilai maksimum yaitu 10.00 dengan rata-rata rating di 6.48.
    3. Jumlah member paling sedikit untuk satu judul anime adalah 16 member dan terbanyak di 1.013.917 member.
    
    Selanjutnya kita melakukan visualisasi distribusi tipe anime menggunakan pie chart dan didapatkan gambaran seperti pada (Gambar 1) berikut:
    
    ![Anime Type Distribution](https://drive.google.com/uc?export=download&id=1Kas9FEpJ2pf73OFTDeI35m5tOx7D9JQy "Anime Type Distribution")
    Gambar 1. Distribusi Tipe Anime
    
    Distribusi tipe anime paling banyak adalah serial TV disusul dengan OVA dan Movie di posisi ke tiga.
2.  Rating Dataset
    Pada Rating Dataset terdapat 7.813.737 baris dan 3 kolom numerikal.
    Kita melakukan data cleansing pada dataset, antara lain senbagai berikut:
    1.  Membuang data untuk rating dengan nilai -1, diketahui bahwa nilai -1 menandakan *user* telah menonton tapi belum memberikan rating
    2.  Membuang duplikasi data dan mengecek nilai Null
    Kemudian mencoba melakukan visualisasi terhadap distribusi rating dan didapatkan gambaran pada (Gambar 2) berikut:
    ![Distribution of Ratings](https://drive.google.com/uc?export=download&id=1bbSLB1jBe3HHpnA-VbYHGiLBD_zft2Ft "Distribution of Ratings")
    Gambar 2. Distribusi Rating

## Data Preparation
Pada tahapan ini ada beberapa teknik data preparation yang dilakukan.
1.  Anime Dataset
    - Kategorisasi pada dataset anime untuk fitur data numerik episodes, rating, dan member untuk mempermudah dalam perhitungan similarity. Dengan membuat kolom baru hasil kategorisasi misal: jumlah episodes menjadi anime_size (very short - epic),
    - Split data gender dan menggabungkannya kembali untuk menstandardkan penulisan data
    - Membuang kolom yang sudah dikategorisasi.
    - Menggabungkan semua kolom yang diperlukan menjadi satu kolom features untuk digunakan pada pembuatan TF-IDF.
    - Langkah terakhir adalah melakukan reset index untuk memperbaiki urutan data.
2.  Rating Dataset
    - Melakukan pengkodean untuk user_id dan anime_id
    - Melakukan normalisasi rating dari skala 0 sampai 1 untuk memudahkan proses training
    - Melakukan Train-Test Split pada data dengan proposi perbandingan 80:20 untuk validasi model.

## Modeling
Dalam tahap ini, akan dibuat dua model sistem rekomendasi, yaitu:
1.  **Content-based filtering (CBF)**
    CBF adalah salah satu teknik dalam sistem rekomendasi yang berfokus pada karakteristik atau konten dari item yang direkomendasikan.
    
    Pada proyek ini dilakukan ekstraksi fitur dengan mengubah data atau informasi item menjadi fitur numerik yang dapat digunakan dalam proses rekomendasi. Fitur (genre, episodes, type, rating, members) digabungkan dan diubah menjadi vektor TF-IDF. Selanjutnya kesamaan item-item yang akan direkomendasikan dihitung menggunakan metrik kesamaan cosine similarity. Metrik ini mengukur sejauh mana vektor vektor fitur item-item cocok satu sama lain. Item-item yang memiliki kesamaan tertinggi diberikan peringkat dan diurutkan. Item-item dengan peringkat tertinggi kemudian direkomendasikan kepada *user*.
    
    Berikut adalah keuntungan dan kekurangan pada teknik ini:
    -  Keuntungan: Kemudahan dalam interpretasi dan dapat diterapkan ketika data yang berasal dari user belum tersedia, karena hanya menggunakan informasi feature yang ada.
    -  Kelemahan: Diperlukan deskripsi item/fitur yang baik untuk teknik ini.
    
    Contoh hasil rekomendasi dapat dilihat pada (Tabel 1).
    
    Tabel. 1 Hasil Rekomendasi Top-5 Anime dengan Teknik CBF 
    Recommendations for **Macross Δ**:
    |No| Name                                   | Sim Score |
    |--|----------------------------------------|----------:|
    |1 | Macross F Movie 1: Itsuwari no Utahime | 0.94      |
    |2 | Macross                                | 0.91      |
    |3 | Macross F                              | 0.91      |
    |4 | Mobile Suit Gundam Seed                | 0.90      |
    |5 | Mobile Suit Gundam Seed Destiny        | 0.90      |

2.  **Collaborative filtering (CF)**
    Kita akan membangun Arsitektur model RecommenderNet yang dirancang untuk mempelajari pola hubungan antara *user_id* dan *anime_id*. Input akan melalui lapisan embedding dan kemudian digabungkan untuk memprediksi preferensi *user* terhadap anime tertentu. Berikut penjelasannya dan cara kerjanya:
    - Fungsi loss Binary Crossentropy digunakan untuk mengukur kesalahan model selama proses pelatihan.
    - Model ini menggunakan Adam Optimizer, yang memungkinkan pembaruan bobot dan bias model berdasarkan gradien, sambil mempertahankan kecepatan dan performa yang baik. Learning rate yang digunakan adalah 0.0001.
    - Metrik yang digunakan untuk evaluasi model adalah MAE (Mean Absolute Error) dan RMSE (Root Mean Squared Error). Penggunaan metrik ini bertujuan untuk mengukur rata-rata selisih antara rating yang diprediksi oleh model dengan rating sebenarnya.
    - batch_size digunakan untuk menentukan jumlah data training yang diproses dalam satu batch sebelum dilakukan penyesuaian bobot model. Semakin besar nilai batch_size, semakin cepat proses pelatihan, namun memori yang digunakan juga semakin besar. Batch Size yang digunakan adalah 256.
    - Epochs menentukan jumlah iterasi di mana seluruh data training diberikan ke model. Semakin banyak epochs, prediksi model cenderung lebih akurat, tetapi juga meningkatkan risiko overfitting. Epochs yang digunakan adalah 8.
    
    Setelah dilatih, model dapat memberikan rekomendasi anime kepada *user* berdasarkan *rating* yang diberikan *user* dengan anime sebelumnya.
    - Keuntungan: Kemampuan untuk memberikan rekomendasi yang dipersonalisasi sesuai dengan preferensi user, serta dapat diterapkan dalam kondisi di mana deskripsi item/feature yang baik tidak tersedia.
    - Kelemahan: Teknik ini memerlukan jumlah data yang besar dari user yang berbeda-beda.

    Berikut adalah contoh hasil dari Sistem Rekomendasi dengan teknik CF:
    ~~~
    Showing recommendations for users: 17440
    ===========================
    Movie with high ratings from user
    --------------------------------
    Code Geass: Hangyaku no Lelouch : Action, Mecha, Military, School, Sci-Fi, Super Power
    Ginga Nagareboshi Gin : Action, Adventure, Drama, Shounen
    Macross F : Action, Mecha, Military, Music, Romance, Sci-Fi, Space
    Pokemon : Action, Adventure, Comedy, Fantasy, Kids
    Code Geass: Nunnally in Wonderland : Comedy, Fantasy, Parody
    --------------------------------
    Top 10 anime recommendation
    --------------------------------
    Kimi no Na wa. : Drama, Romance, School, Supernatural
    Fullmetal Alchemist: Brotherhood : Action, Adventure, Drama, Fantasy, Magic, Military, Shounen
    Gintama° : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Steins;Gate : Sci-Fi, Thriller
    Gintama&#039; : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Hunter x Hunter (2011) : Action, Adventure, Shounen, Super Power
    Ginga Eiyuu Densetsu : Drama, Military, Sci-Fi, Space
    Gintama Movie: Kanketsu-hen - Yorozuya yo Eien Nare : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Gintama&#039;: Enchousen : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    Gintama : Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen
    ~~~

## Evaluation
Pada bagian ini kita akan membahas metrik evaluasi yang digunakan dan hasilnya untuk masing-masing teknik yang digunakan.

### Content-based Filtering

Untuk mengevaluasi Sistem Rekomendasi dengan teknik *Content-based Filtering (CBF)* kita dapat menggunakan *NDCG (Normalized Discounted Cumulative Gain)* setelah sistem rekomendasi ini diimplementasikan.

Gambaran langkah-langkahnya adalah sebagai berikut:
1.  Tentukan skor relevansi untuk setiap judul anime berdasarkan relevansinya dengan *User*.
2.  Buat daftar rekomendasi untuk setiap *User* dalam dataset evaluasi.
3.  Hitung *Discounted Cumulative Gain (DCG)* untuk setiap *User* dengan menjumlahkan skor relevansi $$rel_i$$ dari item-item yang direkomendasikan, yang didiskonkan berdasarkan posisinya $$i$$ dalam daftar $$k$$.
    $$DCG@k = \sum_{i=1}^{k} \frac{rel_i}{\log_2(i+1)}$$
4.  Hitung Ideal DCG (IDCG) untuk setiap *User*, yang mewakili DCG maksimum yang mungkin pada setiap posisi jika daftarnya diurutkan secara sempurna.
5.  Hitung Normalized DCG (NDCG) dengan membagi DCG dengan IDCG pada setiap posisi.
    $$NDCG@k = \frac{DCG@k}{IDCG@k}$$
6. Hitung rata-rata NDCG dari seluruh *User* untuk mengevaluasi performa keseluruhan sistem rekomendasi (jika sudah diimplementasikan dan mendapatkan feedback).

NDCG memberikan ukuran seberapa baik sistem mengurutkan dan merekomendasikan item anime yang relevan. Nilai NDCG yang lebih tinggi menunjukkan performa yang lebih baik, menandakan bahwa item-item yang lebih relevan diurutkan lebih tinggi dalam daftar rekomendasi.

Berdasarkan hasil rekomendasi sebelumnya diberikan skoring relevansi personal untuk judul anime yang direkomendasikan seperti pada (Tabel 2).

Tabel 2. Skoring relevansi terhadap hasil rekomendasi
|No| Name                                   | Sim Score | Relevance Score |
|--|----------------------------------------|----------:|--:|
|1 | Macross F Movie 1: Itsuwari no Utahime | 0.94      | 3 |
|2 | Macross                                | 0.91      | 5 |
|3 | Macross F                              | 0.91      | 4 |
|4 | Mobile Suit Gundam Seed                | 0.90      | 4 |
|5 | Mobile Suit Gundam Seed Destiny        | 0.90      | 3 |

Didapatkan **Nilai NDCG 0.92** pada proyek ini dan ini merupakan pencapaian yang baik (Sistem rekomendasi yang baik memilki nilai NDCG yang mendekati 1.0).

### Collaborative Filtering

Untuk sistem rekomendasi *Collaborative Filtering (CF)*, kita menggunakan 2 metrik evaluasi, yaitu *MAE (Mean Absolute Error)* dan *RMSE (Root Mean Squared Error)*. Berikut adalah formula untuk kedua metrik tersebut:

- $$MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i - \hat{y}_i|$$
- $$RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}$$

Di mana:
- $$n$$ jumlah data (observasi)
- $$y_i$$ nilai aktual
- $$\hat{y}_i$$ nilai prediksi.

Perbedaan antara MAE dan RMSE:
- Cara mengukur perbedaan antara prediksi dan nilai sebenarnya. MAE menghitung rata-rata selisih absolut antara prediksi dan nilai sebenarnya, sedangkan RMSE menghitung akar kuadrat dari rata-rata selisih kuadrat.
- MAE tidak memperhitungkan perbedaan arah, sementara RMSE memberikan penalti lebih besar untuk perbedaan yang lebih besar.
- MAE lebih mudah diinterpretasikan, sementara RMSE lebih sensitif terhadap perbedaan signifikan.

Pada model CF, hasil yang dicapai dapat dilihat pada (Tabel 3) untuk masing-masing grafik training dapat dilihat pada (Gambar 3) dan (Gambar 4).

Tabel 3. Hasil Evaluasi Sistem Rekomendasi dengan Teknik CF
|          | Mean Absolute Error    | Root Mean Squared Error   |
|----------|:------:|:------:|
| Training | 0.1044 | 0.1364 |
| Test     | 0.1048 | 0.1368 |
| Grafik   | ![MAE](https://drive.google.com/uc?export=download&id=1PFOGdncHNk5urVKYWvCCR3F8ChZiGyjz "MAE") Gambar 3. Grafik Training MAE       | ![RMSE](https://drive.google.com/uc?export=download&id=142AeVrCRmKS1GvaEesLYgNXAxH8cDxY8 "RMSE") Gambar 4. Grafik Training RMSE       |

Hasil ini menunjukkan kinerja yang baik untuk sistem rekomendasi.

## Conclusion
Kesimpulan yang dapat diambil dari pembahasan di atas adalah sebagai berikut:
1. Telah dibuat Sistem Rekomendasi dengan teknik ***Content-based Filtering (CBF)*** berdasarkan fitur-fitur yang ada pada dataset Anime Recomendation System (yaitu: genre, episodes, type, rating, dan members) menggunakan *TF-IDF* dan *Cosine Similarity*.
2. Telah dibuat Sistem Rekomendasi dengan teknik ***Collaborative Filtering (CF)*** berdasarkan kemiripan penilaian User terhadap judul Anime yang sudah pernah ditonton sebelumnya dengan membangun *Model Keras* menggunakan *Binary Crossentropy* untuk menghitung *loss function*, Adam (Adaptive Moment Estimation) sebagai *optimizer*, dan Mean Absolute Error (MAE) serta Root Mean Squared Error (RMSE) sebagai *metrics evaluation*. Dihasilkan MAE 0.1048 dan RMSE 0.1368 pada data uji.

Adapun peluang improvement yang dapat dilakukan untuk proyek ini adalah Mengembangkan **Sistem Rekomendasi Hibrida**.

## Daftar Pustaka
[^1] [Masuda, H. et al. (2023). Anime Industry Report 2022. The Association of Japanese Animations.](https://aja.gr.jp/english/japan-anime-data)
[^2] [Murugeswari, R., & Kalaiselvi, M. (2019). Anime Recommendation System Based on Collaborative Filtering and Content-Based Filtering. International Journal of Computer Science and Information Security (IJCSIS).](https://ijcsis.org/papers/vol17no4/A-2637.pdf)
[^3] https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database

**---Ini adalah bagian akhir laporan---**
