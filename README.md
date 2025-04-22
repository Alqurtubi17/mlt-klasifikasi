# **Proyek Deteksi Diabetes**

### **Domain Proyek**
----
Diabetes merupakan salah satu penyakit tidak menular yang berkontribusi besar terhadap angka kematian dan penurunan kualitas hidup di seluruh dunia (Yusnita et al., 2021). Seiring dengan peningkatan angka harapan hidup dan perubahan gaya hidup masyarakat, jumlah penderita diabetes mellitus (DM) diprediksi akan terus meningkat, bahkan mencapai sekitar 578 juta kasus pada tahun 2030 dan melonjak hingga 700 juta kasus pada tahun 2045 (Hasanzad et al., 2022). Kondisi ini menjadi perhatian serius dalam dunia kesehatan global karena dampaknya yang kompleks terhadap individu maupun sistem pelayanan kesehatan.

Oleh karena itu, deteksi dini dan prediksi risiko diabetes menjadi langkah strategis yang sangat penting untuk mengurangi potensi komplikasi serta meningkatkan kualitas hidup pasien (Saputro et al., 2024). Permasalahan utama yang dihadapi saat ini adalah bagaimana memanfaatkan data klinis yang tersedia untuk mengidentifikasi individu dengan risiko tinggi secara akurat dan efisien. Prediksi yang tepat tidak hanya dapat membantu dalam pengambilan keputusan medis, tetapi juga mampu menekan biaya pelayanan kesehatan dengan memungkinkan intervensi preventif yang lebih cepat.

Namun, tantangan dalam membangun sistem prediksi yang andal cukup kompleks. Di antaranya adalah pemilihan fitur yang paling relevan dari data kesehatan yang beragam, mengatasi risiko overfitting dan underfitting dalam model prediktif, serta menentukan algoritma machine learning yang paling tepat digunakan dalam konteks klinis tertentu (Hovi et al., 2022). 

Melihat ketersediaan data kesehatan yang semakin luas, pendekatan berbasis machine learning menjadi alternatif potensial untuk membantu tenaga medis dalam melakukan prediksi risiko diabetes secara lebih objektif dan presisi. Berbagai studi sebelumnya telah menunjukkan keberhasilan penerapan algoritma machine learning untuk tujuan ini, seperti penelitian oleh Widodo et al. (2021) yang menggunakan logistic regression dan memperoleh akurasi sebesar 92,3%, serta Apriliah et al. (2021) yang menerapkan random forest dan mencatatkan akurasi sebesar 97,88%. 

Berdasarkan latar belakang tersebut, proyek ini bertujuan untuk membangun sistem prediksi diabetes dengan memanfaatkan berbagai variabel klinis seperti usia, indeks massa tubuh (BMI), riwayat hipertensi, penyakit jantung, kadar HbA1c, serta riwayat merokok. Dengan pendekatan machine learning yang tepat, sistem ini diharapkan dapat memberikan hasil prediksi yang akurat dan dapat diandalkan sebagai alat bantu pengambilan keputusan dalam dunia medis.

### **Business Understanding**
---
- **Problem Statements**
    1. Apa fitur yang paling berpengaruh terhadap prediksi risiko diabetes?

    2. Algoritma machine learning mana yang paling efektif dalam memprediksi risiko diabetes pada dataset yang tersedia?

- **Goals**
    1. Mengembangkan model prediktif yang mampu mengklasifikasikan individu berisiko diabetes dengan akurasi tinggi.

    2. Membandingkan performa tiga algoritma klasifikasi (Random Forest, XGBoost, dan Logistic Regression) untuk menentukan model terbaik berdasarkan metrik evaluasi seperti akurasi, precision, recall, dan F1-score.

    3. Mengetahui fitur apa saja yang paling berpengaruh dalam mengklasifikasikan individu berisiko diabetes.

- **Solution Statements**
    1. Membangun pipeline machine learning lengkap mulai dari EDA, preprocessing, hingga evaluasi model.

    2. Mengimplementasikan tiga algoritma klasifikasi: Random Forest, XGBoost, dan Logistic Regression.

    3. Melakukan scaling dan encoding fitur serta balancing data dan hyperparameter tuning untuk meningkatkan performa model.

    4. Menggunakan metrik klasifikasi (accuracy, precision, recall, F1-score) sebagai alat evaluasi dan pemilihan model terbaik.

    5. Menggunakan analisis feature importance untuk mengetahui variabel-variabel yang paling berpengaruh dalam proses klasifikasi.

### **Data Understanding**
---
Proyek ini menggunakan [**Diabetes Prediction Dataset**](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset/data) merupakan kumpulan data medis dan demografis dari pasien, yang dilengkapi dengan status diabetes (positif atau negatif). Dataset ini mencakup berbagai fitur penting yang dapat digunakan untuk membantu memprediksi risiko diabetes berdasarkan karakteristik individu.

Fitur-fitur dalam dataset ini meliputi:

- **gender**: Jenis kelamin pasien (Female, Male, Other).

- **age**: Usia pasien dalam tahun.

- **hypertension**: Riwayat hipertensi (1 = memiliki hipertensi, 0 = tidak).

- **heart_disease**: Riwayat penyakit jantung (1 = memiliki, 0 = tidak).

- **smoking_history**: Riwayat merokok pasien, termasuk kategori seperti never, former, current, ever, not current, dan No Info.

- **bmi**: Indeks massa tubuh, yang dihitung dari berat badan dan tinggi badan.

- **HbA1c_level**: Kadar hemoglobin A1c, yang menggambarkan rata-rata kadar gula darah dalam beberapa bulan terakhir.

- **blood_glucose_level**: Kadar gula darah pasien saat ini.

- **diabetes**: Label target, menunjukkan apakah pasien menderita diabetes (1) atau tidak (0).

Dataset prediksi diabetes terdiri dari 100.000 baris data dengan 9 kolom yang merepresentasikan informasi medis dan demografis pasien. Seluruh kolom tidak memiliki nilai kosong (missing values).

| No | Kolom                 | Tipe Data | Non-Null Count |
|----|-----------------------|-----------|----------------|
| 1  | `gender`              | object    | 100,000        |
| 2  | `age`                 | float64   | 100,000        |
| 3  | `hypertension`        | int64     | 100,000        |
| 4  | `heart_disease`       | int64     | 100,000        |
| 5  | `smoking_history`     | object    | 100,000        |
| 6  | `bmi`                 | float64   | 100,000        |
| 7  | `HbA1c_level`         | float64   | 100,000        |
| 8  | `blood_glucose_level` | int64     | 100,000        |
| 9  | `diabetes`            | int64     | 100,000        |

Untuk memastikan kualitas data, dilakukan pemeriksaan apakah terdapat baris data yang sama persis (duplikat) dan dataset tidak memiliki nilai yang hilang (missing values) dalam dataset.

```python
# Cek duplicate
print("\n=== Duplicate Values ===")
print(df.duplicated().sum())

Output:
=== Duplicate Values ===  
3854
```
Terdapat 3.854 baris duplikat dalam dataset yang perlu dihapus agar tidak memengaruhi hasil analisis dan pemodelan secara negatif.

```python
# Cek missing values
print("\n=== Missing Values ===")
print(df.isnull().sum())

Output:
=== Missing Values ===
gender                 0
age                    0
hypertension           0
heart_disease          0
smoking_history        0
bmi                    0
HbA1c_level            0
blood_glucose_level    0
diabetes               0
```
Hasil di atas menunjukkan bahwa tidak terdapat missing values dalam dataset ini. Dengan demikian, tidak diperlukan proses imputasi atau penghapusan data.

Setelah proses data understanding selesai dilakukan, langkah selanjutnya adalah eksplorasi data atau Exploratory Data Analysis (EDA). Tahapan ini bertujuan untuk memahami pola, hubungan, serta karakteristik dari setiap fitur dalam dataset, baik dari sisi distribusi masing-masing variabel (univariat) maupun hubungan antar variabel (multivariat). Dengan melakukan EDA, kita dapat mengidentifikasi potensi outlier, ketidakseimbangan kelas, dan variabel-variabel yang berpengaruh terhadap target prediksi, yaitu diabetes.

![Gambar 1. Sebaran Diabetes](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image.png?raw=true)
Distribusi target diabetes sangat tidak seimbang, dengan mayoritas individu dikategorikan sebagai non-diabetes (0) dan hanya sebagian kecil yang didiagnosis diabetes (1). Hal ini menunjukkan adanya potensi masalah class imbalance yang perlu ditangani saat proses pemodelan, misalnya dengan teknik SMOTETomek untuk penyeimbangan data.

![Gambar 2. Distribusi Variabel Numerik](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-2.png?raw=true)
Analisis univariat terhadap fitur numerik dalam dataset dilakukan untuk memahami distribusi, rentang, dan kecenderungan nilai dari setiap variabel. Distribusi kadar glukosa, misalnya, menunjukkan penyebaran yang luas dengan puncak frekuensi yang berada pada rentang antara 90 hingga 150 mg/dL. Hal ini mengindikasikan bahwa sebagian besar individu dalam populasi cenderung memiliki kadar glukosa dalam kisaran normoglikemia hingga ambang hiperglikemia. Variabel indeks massa tubuh (BMI) memperlihatkan kecenderungan distribusi yang miring ke kanan, dengan mayoritas individu berada pada rentang 25–35 kg/m², yang menunjukkan bahwa populasi memiliki dominasi berat badan berlebih hingga obesitas. Usia memiliki distribusi unimodal dengan penyebaran dari usia muda hingga lanjut, dan konsentrasi frekuensi berada di sekitar rentang 40–60 tahun. Tekanan darah juga menunjukkan distribusi normal yang agak menyebar, dengan nilai yang banyak muncul pada kisaran 70–85 mmHg (diasumsikan sebagai tekanan diastolik atau rerata tekanan darah).

![Gambar 3. Sebaran Variabel Kategorik](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-3.png?raw=true)
Analisis univariat fitur kategorikal bertujuan untuk memahami distribusi proporsi setiap kategori dalam populasi tanpa mengaitkannya dengan variabel target. Pada fitur jenis kelamin (gender), distribusi terbagi ke dalam tiga kategori: Female, Male, dan Other. Mayoritas responden adalah Female dan Male, dengan jumlah relatif seimbang, sementara kategori Other memiliki proporsi yang sangat kecil, mencerminkan keberadaan individu non-biner atau data yang tidak diklasifikasikan secara tradisional. Fitur riwayat merokok (smoking_history) memiliki enam kategori: never, no info, current, former, ever, dan not current. Kategori never mendominasi distribusi, menunjukkan sebagian besar responden tidak pernah merokok. Diikuti oleh kategori former dan ever, yang menunjukkan riwayat merokok di masa lalu, serta current, yang mewakili perokok aktif. not current tampaknya digunakan untuk mengklasifikasikan individu yang saat ini tidak merokok, meskipun pernah, sementara no info menunjukkan data tidak tersedia atau tidak dijawab. Keberadaan kategori seperti no info penting untuk dicermati karena dapat merepresentasikan ketidaklengkapan data. Fitur hipertensi (hypertension) hanya memiliki dua kategori: yes dan no, dengan mayoritas responden tidak memiliki riwayat hipertensi (no). Sementara itu, fitur penyakit jantung (heart_disease) juga terdiri dari dua kategori: yes dan no, dan secara umum menunjukkan proporsi yang lebih besar pada kategori no, mengindikasikan bahwa sebagian besar individu dalam populasi ini tidak memiliki riwayat penyakit jantung.

![Gambar 4. Korelasi](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-4.png?raw=true)
Berdasarkan heatmap korelasi Pearson, variabel HbA1c dan glukosa darah menunjukkan korelasi tertinggi terhadap status diabetes, masing-masing sekitar +0,42 dan +0,4, menjadikannya indikator klinis utama dalam prediksi diabetes. Indeks massa tubuh (BMI) memiliki korelasi sedang, sekitar +0,21, diikuti oleh hipertensi dan usia, masing-masing sekitar +0,2 dan +0,26. Korelasi dengan penyakit jantung rendah, sekitar 0,17. Korelasi antar variabel input tidak menunjukkan nilai ekstrem, sehingga tidak terdapat indikasi multikolinearitas yang signifikan dalam data.

![Gambar 5. Rokok - Diabetes](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-5.png?raw=true)
Dari grafik, tampak bahwa proporsi individu dengan diabetes lebih tinggi pada kelompok perokok aktif dibandingkan dengan bukan perokok. Hal ini mengindikasikan adanya potensi asosiasi positif antara kebiasaan merokok dan kejadian diabetes. Merokok dapat memicu resistensi insulin melalui stres oksidatif dan peradangan kronis yang mengganggu metabolisme glukosa. Oleh karena itu, merokok dapat dianggap sebagai faktor risiko tambahan yang berkontribusi terhadap munculnya diabetes tipe 2.

![Gambar 6. Gender - Diabetes](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-6.png?raw=true)
Dari visualisasi yang disajikan, tidak terlihat perbedaan yang mencolok antara laki-laki dan perempuan dalam hal prevalensi diabetes. Ini menunjukkan bahwa jenis kelamin mungkin bukan faktor determinan utama dalam model prediksi diabetes pada dataset ini. Namun, dari perspektif epidemiologis, perbedaan hormonal dan gaya hidup antara laki-laki dan perempuan tetap dapat berpengaruh secara tidak langsung terhadap sensitivitas insulin dan regulasi glukosa darah, sehingga tetap relevan sebagai variabel demografis.

![Gambar 7. BMI - Diabetes](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-7.png?raw=true)
Terlihat bahwa individu dengan nilai BMI tinggi memiliki kecenderungan lebih besar untuk menderita diabetes. Hubungan ini konsisten dengan temuan dalam literatur medis, yang menyatakan bahwa obesitas sentral merupakan salah satu kontributor utama resistensi insulin. Akumulasi jaringan adiposa, terutama lemak visceral, menghasilkan sitokin proinflamasi yang mengganggu homeostasis glukosa.

![Gambar 8. Usia - Diabetes](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-8.png?raw=true)
Tampak bahwa prevalensi diabetes meningkat secara progresif seiring bertambahnya usia. Hal ini sejalan dengan teori fisiologis yang menyatakan bahwa sensitivitas insulin menurun dengan bertambahnya usia akibat perubahan komposisi tubuh, penurunan massa otot, serta peningkatan stres metabolik. Secara statistik, usia menjadi salah satu prediktor penting dalam model klasifikasi diabetes, karena mencerminkan akumulasi risiko sepanjang hidup individu.

Sebelum masuk ke tahap modeling, dilakukan analisis statistik deskriptif terhadap variabel numerik dalam dataset untuk memahami distribusi data secara umum. Statistik ini mencakup jumlah data, nilai rata-rata, standar deviasi, nilai minimum dan maksimum, serta kuartil pertama (Q1), median (Q2), dan kuartil ketiga (Q3).


|                      | age       | hypertension | heart_disease | bmi       | HbA1c_level | blood_glucose_level | diabetes  |
|----------------------|-----------|--------------|----------------|-----------|--------------|----------------------|------------|
| **count**            | 100000 | 100000 | 100000  | 100000 | 100000 | 100000         | 100000 |
| **mean**             | 41.89     | 0.07485      | 0.039420       | 27.32     | 5.53         | 138.06               | 0.085000       |
| **std**              | 22.52     | 0.26315      | 0.194593       | 6.64      | 1.07         | 40.71                | 0.278883       |
| **min**              | 0.08      | 0.00000      | 0.000000       | 10.01     | 3.50         | 80.00                | 0.000000       |
| **25% (Q1)**         | 24.00     | 0.00000      | 0.000000       | 23.63     | 4.80         | 100.00               | 0.000000       |
| **50% (Median)**     | 43.00     | 0.00000      | 0.000000       | 27.32     | 5.80         | 140.00               | 0.000000       |
| **75% (Q3)**         | 60.00     | 0.00000      | 0.000000       | 29.58     | 6.20         | 159.00               | 0.000000       |
| **max**              | 80.00     | 1.00000      | 1.000000       | 95.69     | 9.00         | 300.00               | 1.000000       |

### **Data Preparation**
Tahapan data preparation merupakan proses penting dalam memastikan data yang digunakan dalam machine learning sudah bersih, representatif, dan siap untuk diproses. Berikut rangkaian langkah yang dilakukan:
```python 
# Hapus duplikat
df.drop_duplicates(inplace=True)
```
Langkah awal dilakukan dengan mengecek dan menghapus data duplikat menggunakan df.drop_duplicates(inplace=True). Dari total data, ditemukan sebanyak 3.854 baris duplikat yang dapat menyebabkan bias model dan overfitting jika tidak dihapus. Penghapusan ini penting untuk meningkatkan kualitas dan representasi data agar tidak ada informasi yang dihitung lebih dari sekali.
```python 
# Hapus gender 'Other' 
df = df[df['gender'].isin(['Male', 'Female'])]
```
Kolom gender memiliki tiga nilai unik: "Male", "Female", dan "Other", kategori ini dihapus menggunakan filter df[df['gender'].isin(['Male', 'Female'])]. Penghapusan ini dilakukan agar model tidak terdistraksi oleh kategori yang tidak signifikan secara statistik dan menghindari noise yang bisa mengganggu proses pelatihan
```python 
# Hapus baris dengan nilai 'No Info' di kolom smoking_history
df = df[df['smoking_history'] != 'No Info']
```
Pada kolom smoking_history, nilai "No Info" merepresentasikan missing value terselubung, data ini dihapus menggunakan filter df[df['smoking_history'] != 'No Info']. Tujuan penghapusan ini adalah untuk membersihkan data dari informasi yang tidak jelas dan tidak informatif, sehingga model dapat lebih fokus pada pola-pola yang benar-benar relevan.
```python 
# Encode variabel kategorikal
df_encoded = df.copy()
le_gender = LabelEncoder()
le_smoking = LabelEncoder()
df_encoded['gender'] = le_gender.fit_transform(df_encoded['gender'])
df_encoded['smoking_history'] = le_smoking.fit_transform(df_encoded['smoking_history'])
```
Untuk mengubah data kategorikal menjadi format numerik, dilakukan proses label encoding pada kolom gender dan smoking_history menggunakan LabelEncoder. Ini penting karena algoritma machine learning membutuhkan input dalam bentuk numerik. Sebagai hasilnya, kategori "Male" dan "Female" dikodekan sebagai 1 dan 0, sedangkan nilai unik pada smoking_history seperti "never", "current", "former", dll. juga dikodekan menjadi angka. Ini membuat data siap untuk digunakan dalam proses pelatihan model.
```python 
# Pisahkan fitur dan target
X = df_encoded.drop('diabetes', axis=1)
y = df_encoded['diabetes']

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```
Data dipisahkan menjadi fitur (X) dan target (y), kemudian dibagi menjadi 80% data latih dan 20% data uji menggunakan train_test_split. Pembagian ini bertujuan untuk mengevaluasi kemampuan model dalam mengeneralisasi data baru. Proses ini juga membantu mencegah overfitting karena evaluasi dilakukan pada data yang belum pernah dilihat oleh model sebelumnya.
```python 
# Standardisasi fitur numerik
scaler = RobustScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```
Scaling dilakukan menggunakan RobustScaler yang lebih tahan terhadap outlier dibanding metode lainnya. Fitur numerik pada X_train dan X_test dinormalisasi agar berada dalam rentang skala yang seragam. Ini penting karena beberapa algoritma seperti Logistic Regression sangat sensitif terhadap perbedaan skala antar fitur.
```python 
# Balancing 
sm = SMOTETomek(random_state=0)
X_train_resampled, y_train_resampled = sm.fit_resample(X_train_scaled, y_train)

print("\nDistribusi kelas sebelum SMOTETomek:", Counter(y_train))
print("Distribusi kelas sesudah SMOTETomek:", Counter(y_train_resampled))

Output:
Distribusi kelas sebelum SMOTETomek: Counter({0: 44892, 1: 5705})
Distribusi kelas sesudah SMOTETomek: Counter({0: 44414, 1: 44414})
```
Distribusi target diabetes yang tidak seimbang diatasi menggunakan teknik kombinasi SMOTE (Synthetic Minority Oversampling Technique) dan Tomek Links. Dengan sm.fit_resample(X_train_scaled, y_train), data kelas minoritas disintesis dan sampel ambigu dibersihkan. Setelah balancing, distribusi kelas menjadi lebih seimbang, yang sangat penting untuk menghindari bias prediksi terhadap kelas mayoritas serta meningkatkan metrik evaluasi seperti recall dan F1-score.

### **Modelling dan Hyperparameter Tuning**
---
Setelah melalui proses pembersihan data, pengkodean fitur, dan penskalaan nilai-nilai numerik, data kemudian dibagi menjadi training set dan testing set dengan rasio 80:20 untuk memastikan evaluasi model yang adil. Namun, karena terdapat ketidakseimbangan kelas pada target (diabetes), dilakukan penyeimbangan data menggunakan SMOTETomek, yaitu kombinasi teknik oversampling pada kelas minoritas dan undersampling pada kelas mayoritas secara bersamaan, guna memperbaiki distribusi kelas dan meningkatkan performa model.

Selanjutnya, proses pemodelan dilakukan dengan tiga algoritma machine learning yang berbeda, yaitu Random Forest, XGBoost, dan Logistic Regression. Ketiga algoritma ini dipilih karena memiliki keunggulan masing-masing dalam hal akurasi, interpretabilitas, dan kemampuan menangkap hubungan non-linear.

Untuk memastikan setiap model bekerja secara optimal, dilakukan hyperparameter tuning menggunakan metode GridSearchCV, yaitu pencarian kombinasi parameter terbaik berdasarkan validasi silang (cross-validation) 3-fold. Hal ini bertujuan untuk mengurangi risiko overfitting dan memperoleh model dengan kinerja terbaik pada data yang belum pernah dilihat sebelumnya.

1. Logistic Regression (LR)
    
    Logistic Regression adalah model linier untuk klasifikasi yang memprediksi probabilitas suatu data termasuk dalam kelas tertentu (biasanya kelas 1).

    Model menghitung kombinasi linier dari fitur:

    $$ z = \beta_0 + \beta_1x_1 + \beta_2x_2 + ... + \beta_nx_n $$

    Nilai ini kemudian dilewatkan ke fungsi sigmoid untuk menghasilkan probabilitas antara 0 dan 1:

    $$ P(y=1 \mid x) = \frac{1}{1 + e^{-x}}$$

    Jika probabilitas > 0.5, maka prediksi = 1, sebaliknya prediksi = 0.

    Logistic Regression di proyek ini menggunakan dua parameter utama dalam proses tuning, yaitu C dan solver. Berikut penjelasannya:

    ```python
    # Logistic Regression
    lr_params = {
        'C': [0.1, 1.0, 10.0],
        'solver': ['lbfgs', 'liblinear']
    }
    lr = GridSearchCV(LogisticRegression(max_iter=1000, random_state=42, class_weight='balanced'), lr_params, cv=3, n_jobs=-1)
    ```
    - C (Inverse of Regularization Strength)
        
        Parameter ini mengontrol kekuatan regularisasi. Nilai C yang lebih kecil akan memberikan regularisasi yang lebih kuat, artinya model menjadi lebih sederhana dan cenderung menghindari overfitting. Sebaliknya, nilai C yang lebih besar membuat model lebih fleksibel, namun lebih berisiko overfit jika data terlalu kompleks. Nilai yang diuji: 0.1, 1.0, dan 10.0.

    - solver (Optimization Algorithm)
        
        Solver menentukan metode optimisasi yang digunakan untuk mencari parameter terbaik.
        - 'liblinear': Cocok untuk dataset kecil sampai menengah dan mendukung regularisasi L1 dan L2.
        -  'lbfgs': Lebih efisien untuk dataset besar dan digunakan untuk regularisasi L2.
    
    GridSearch akan memilih parameter terbaik berdasarkan hasil validasi silang 3-fold.

    Kelebihan:
    - Sederhana dan cepat dalam pelatihan serta interpretasi.
    - Cocok untuk baseline model dan data yang relatif linear.
    - Hasil model mudah dijelaskan, sehingga cocok untuk data medis yang membutuhkan interpretabilitas.

    Kekurangan:
    - Tidak mampu menangkap hubungan non-linear antar variabel.
    - Kurang akurat jika data kompleks dan memiliki banyak interaksi antar fitur.

    Improvement:
    - Dilakukan hyperparameter tuning seperti pemilihan solver (liblinear, lbfgs) dan regularisasi (C).

2. Random Forest (RF)

    Random Forest adalah ensemble dari banyak pohon keputusan (decision trees) yang digabungkan untuk meningkatkan akurasi dan mengurangi overfitting.

    Langkah-langkah utama:

    1. Bangun banyak decision tree (misal 100–150).

    2. Untuk setiap pohon:

        - Gunakan subset data (bootstrap sample).
        - Di setiap split, pilih subset acak dari fitur.

    3. Setiap pohon menghasilkan prediksi.

    4. Hasil akhir diambil dari mayoritas suara (voting) dari seluruh pohon.

    Tidak ada satu rumus eksplisit, tapi setiap pohon mengikuti pembentukan split berdasarkan Information Gain / Gini Impurity, misalnya:

    $$ \text{Gini}(t) = 1 - \sum_{i=1}^{C} {p_i^2} $$

    Di mana $p_i$ adalah proporsi kelas ke-i pada node t.

    Rumus Random Forest untuk klasifikasi:

    Misalkan $T_1(x),T_2(x),\ldots, T_k(x)$ adalah prediksi dari masing-masing pohon, maka prediksi akhir $\hat{y}$ adalah

    $$\hat{y} = \text{mode} \left( T_1(x), T_2(x), \ldots, T_K(x) \right)$$

    Random Forest adalah algoritma ensemble yang menggunakan banyak pohon keputusan. Parameter tuning dilakukan terhadap n_estimators, max_depth, dan min_samples_split.

    ```python
    # Random Forest
    rf_params = {
        'n_estimators': [100, 150],
        'max_depth': [None, 10],
        'min_samples_split': [2, 5]
    }
    rf = GridSearchCV(RandomForestClassifier(random_state=42, class_weight='balanced'), rf_params, cv=3, n_jobs=-1)
    ```
    - n_estimators (Number of Trees)
    
        Jumlah pohon dalam hutan. Semakin banyak pohon, hasil prediksi cenderung lebih stabil dan akurat, tetapi waktu pelatihan juga meningkat. Nilai yang diuji: 100 dan 150.

    - max_depth (Maximum Depth of Each Tree)
        
        Mengontrol kedalaman maksimum dari setiap pohon.
        - Jika diatur ke None, maka pohon akan terus tumbuh hingga semua daun adalah pure (berisi satu kelas saja), yang bisa menyebabkan overfitting.
        - Dengan membatasi kedalaman (misalnya 10), model jadi lebih sederhana dan cenderung lebih general.

    - min_samples_split (Minimum Samples to Split a Node)

        Menentukan jumlah minimum sampel yang diperlukan untuk membagi node internal.
        - Nilai kecil (misalnya 2) memungkinkan pembagian yang lebih sering dan pohon lebih kompleks.
        - Nilai lebih besar (misalnya 5) mengurangi kompleksitas model dan membantu menghindari overfitting.

    GridSearch akan memilih parameter terbaik berdasarkan hasil validasi silang 3-fold.

    Kelebihan:
    - Mampu menangkap hubungan non-linear dan interaksi antar fitur.
    - Robust terhadap outlier dan data imbalance.
    - Memberikan feature importance secara langsung.

    Kekurangan:
    - Model lebih kompleks dan membutuhkan lebih banyak memori dan waktu pelatihan.
    - Tidak sebaik XGBoost dalam hal akurasi pada dataset besar atau rumit.

    Improvement:
    - Dilakukan tuning terhadap parameter seperti n_estimators, max_depth, dan min_samples_split untuk mendapatkan model terbaik.

3. XGBoost (Extreme Gradient Boosting)

    XGBoost adalah algoritma boosting berbasis pohon yang membangun model secara bertahap, di mana setiap pohon baru dibuat untuk memperbaiki kesalahan dari pohon-pohon sebelumnya. Model dioptimalkan dengan fungsi objektif yang terdiri dari fungsi loss dan regularisasi untuk menghindari overfitting. Cara kerja dari XGBoost adalah sebagai berikut:

    1. Model awal memulai dari prediksi konstan (misal rata-rata).
    2. Pohon baru ditambahkan untuk meminimalkan error sisa dari model sebelumnya.
    3. Proses ini dilakukan secara iteratif sampai jumlah pohon tertentu tercapai atau error tidak berkurang lagi secara signifikan.
    4. XGBoost menggunakan regularisasi (L1/L2) untuk mengendalikan kompleksitas pohon.

    Fungsi Objektif XGBoost:
    $$\mathcal{L}(\phi) = \sum_{i=1}^{n} l\left(y_i, \hat{y}_i^{(t)}\right) + \sum_{k=1}^{t} \Omega(f_k)$$

    dimana:
    - $l\left(y_i, \hat{y}_i^{(t)}\right)$: fungsi loss (contoh: log loss untuk klasifikasi).
    - $\Omega(f) = \gamma T + \frac{1}{2} \lambda \sum_{j=1}^{T} w_j^2$:  fungsi regularisasi untuk menghindari overfitting, di mana $T$ adalah jumlah daun dalam pohon dan $w_j$ adalah skor setiap daun.
    - $\hat{y}_i^{(t)} = \sum_{k=1}^{t} f_k(x_i)$: prediksi kumulatif hingga pohon ke-$t$.

    XGBoost merupakan algoritma boosting yang sangat powerful dan fleksibel. Parameter tuning dilakukan terhadap n_estimators, max_depth, dan learning_rate.

    ```python
    # XGBoost
    xgb_params = {
        'n_estimators': [100, 150],
        'max_depth': [3, 5],
        'learning_rate': [0.1, 0.3]
    }
    xgb = GridSearchCV(XGBClassifier(use_label_encoder=False, eval_metric='logloss', random_state=42), xgb_params, cv=3, n_jobs=-1)
    ```

    - n_estimators (Number of Boosting Rounds)
        
        Menentukan jumlah pohon yang akan dibangun secara berurutan. Sama seperti Random Forest, semakin banyak pohon, potensi akurasi meningkat, tetapi juga berisiko overfit jika tidak dikontrol.

    - max_depth (Depth of Each Tree)
        
        Mengatur kedalaman maksimal dari pohon.
        - Nilai kecil seperti 3 membuat model lebih sederhana dan general.
        - Nilai yang lebih besar seperti 5 memungkinkan model mempelajari hubungan lebih kompleks, tetapi berpotensi overfitting jika tidak diimbangi dengan regulasi lain.

    - learning_rate (Step Size Shrinkage / η)
        
        Parameter penting dalam boosting yang menentukan seberapa besar kontribusi setiap pohon terhadap prediksi akhir.
        - Nilai yang kecil (misalnya 0.1) membuat model belajar lebih perlahan tapi hasil akhirnya lebih stabil.
        - Nilai yang lebih besar (0.3) membuat model belajar lebih cepat, tetapi jika terlalu besar bisa melewatkan solusi optimal.

    GridSearch akan memilih parameter terbaik berdasarkan hasil validasi silang 3-fold.

    Kelebihan:
    - Sangat powerful dalam menangani dataset besar dan kompleks.
    - Memiliki fitur regulasi bawaan yang membantu menghindari overfitting.
    - Umumnya menghasilkan akurasi terbaik dibanding algoritma lain.

    Kekurangan:
    - Waktu pelatihan lebih lama dibanding Logistic Regression.
    - Lebih kompleks dan membutuhkan tuning parameter secara hati-hati.

    Improvement:
    - Tuning dilakukan terhadap learning_rate, max_depth, n_estimators, dan subsample.

Setiap model dilatih dengan data training yang telah dibalancing dan distandarisasi. Evaluasi awal dilakukan dengan data testing untuk mendapatkan nilai Accuracy, Precision, Recall, dan F1 Score.

### **Evaluation**
---
Evaluasi model bertujuan untuk mengukur sejauh mana performa algoritma dalam memprediksi risiko diabetes berdasarkan fitur kesehatan dan gaya hidup pasien. Dalam proyek ini, digunakan beberapa metrik evaluasi klasifikasi yang sangat penting untuk menilai efektivitas model, khususnya dalam konteks medis di mana akurasi semata tidak cukup. Dalam klasifikasi biner, model membuat dua jenis prediksi: positif (1) dan negatif (0). Hasil dari prediksi model dapat dikategorikan ke dalam empat kelompok berdasarkan kesesuaian dengan label aktual. Empat kategori tersebut adalah:

1. True Positive (TP)

    Model memprediksi positif, dan hasil yang sebenarnya juga positif.
    
    Contoh: Model memprediksi seseorang menderita diabetes, dan kenyataannya orang tersebut memang menderita diabetes.

2. False Positive (FP)
    
    Model memprediksi positif, tetapi hasil yang sebenarnya adalah negatif.

    Contoh: Model memprediksi seseorang menderita diabetes, padahal orang tersebut tidak menderita diabetes. Ini disebut juga Type I Error.

3. True Negative (TN)

    Model memprediksi negatif, dan hasil yang sebenarnya juga negatif.

    Contoh: Model memprediksi seseorang tidak menderita diabetes, dan kenyataannya orang tersebut memang tidak menderita diabetes.

4. False Negative (FN)

    Model memprediksi negatif, tetapi hasil yang sebenarnya adalah positif.

    Contoh: Model memprediksi seseorang tidak menderita diabetes, padahal orang tersebut sebenarnya menderita diabetes. Ini disebut juga Type II Error.

Adapun metrik evaluasi yang digunakan antara lain:
1. **Accuracy**

    **Accuracy** mengukur proporsi jumlah prediksi yang benar terhadap seluruh jumlah prediksi.

    $$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

    **Kelebihan**: Cocok untuk data yang seimbang.  
    **Kekurangan**: Dapat menyesatkan jika data tidak seimbang (misalnya kasus positif jauh lebih sedikit dari negatif).


2. **Precision**

    **Precision** mengukur seberapa akurat model saat memprediksi kelas positif (diabetes).

    $$\text{Precision} = \frac{TP}{TP + FP}$$

    **Kelebihan**: Berguna ketika kesalahan positif (false positive) harus diminimalkan.  
    **Dalam konteks medis**: Precision tinggi berarti lebih sedikit pasien sehat yang salah diklasifikasikan sebagai penderita diabetes.


3. **Recall** (Sensitivity)

    **Recall** mengukur seberapa baik model mendeteksi semua kasus positif aktual.

    $$\text{Recall} = \frac{TP}{TP + FN}$$

    **Kelebihan**: Penting ketika false negative harus diminimalkan.  
    **Dalam konteks medis**: Recall tinggi sangat penting karena kita ingin menangkap sebanyak mungkin pasien yang benar-benar berisiko diabetes.

4. **F1 Score**

    **F1 Score** adalah rata-rata harmonik dari precision dan recall.

    $$\text{F1 Score} = 2 \times \frac{(\text{Precision} \times \text{Recall})}{(\text{Precision} + \text{Recall})}$$

    **Kelebihan**: Memberikan keseimbangan antara precision dan recall, sangat efektif untuk data tidak seimbang.

Setelah dilakukan pelatihan dan tuning, diperoleh hasil sebagai berikut:

| Model               | Accuracy | Precision | Recall | F1 Score | Best Params |
|--------------------|----------|-----------|--------|----------|-------------|
| Random Forest       | 0.9492   | 0.7660    | 0.7447 | 0.7552   | {'max_depth': None, 'min_samples_split': 2, 'n_estimators': 150} |
| **XGBoost (Terbaik)** | **0.9600**   | **0.8896**    | **0.7080** | **0.7885**   | {'learning_rate': 0.3, 'max_depth': 5, 'n_estimators': 150} |
| Logistic Regression | 0.8760   | 0.4531    | 0.8604 | 0.5936   | {'C': 0.1, 'solver': 'liblinear'} |


Dari tabel di atas, dapat disimpulkan bahwa XGBoost merupakan model dengan performa terbaik karena memberikan nilai F1 score tertinggi (0.7885), yang menandakan keseimbangan yang baik antara precision dan recall. Model ini juga memiliki precision tertinggi (0.8896), yang berarti model sangat jarang melakukan false positive, serta tetap mampu menjaga recall yang cukup baik Logistic Regression memiliki recall yang tinggi, namun precision-nya sangat rendah sehingga kurang ideal untuk digunakan sebagai model utama. Sementara Random Forest memberikan hasil yang seimbang, namun masih berada di bawah XGBoost dalam semua metrik utama.

![Gambar 10. Confusion Matrix XGBoost](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-9.png?raw=true)

Berdasarkan confusion matrix dari model XGBoost, dilakukan perhitungan metrik evaluasi menggunakan rumus-rumus standar untuk klasifikasi biner. Akurasi dihitung sebagai proporsi prediksi benar terhadap seluruh prediksi, yaitu:
$$
\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} 
$$
$$= \frac{943 + 11201}{943 + 11201 + 117 + 389} = \frac{12144}{12650} \approx 0.9600 \text{ atau } 96.00\%
$$
Hasil ini menunjukkan bahwa 96% dari seluruh sampel berhasil diklasifikasikan dengan benar oleh model.
$$
\text{Precision} = \frac{TP}{TP + FP} = \frac{943}{943 + 117} = \frac{943}{1060} \approx 0.8896 \text{ atau } 88.96\%
$$
Artinya, dari seluruh individu yang diprediksi mengidap diabetes, sekitar 89% memang benar-benar positif.
$$
\text{Recall} = \frac{TP}{TP + FN} = \frac{943}{943 + 389} = \frac{943}{1332} \approx 0.7081 \text{ atau } 70.81\%
$$
Nilai ini menunjukkan bahwa model berhasil mengidentifikasi sekitar 71% dari seluruh kasus diabetes aktual, namun masih melewatkan sebagian (false negative = 389).
$$
\text{F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} 
$$
$$= 2 \times \frac{0.8896 \times 0.7081}{0.8896 + 0.7081} \approx \frac{1.259}{1.5977} \approx 0.7872 \text{ atau } 78.72\%
$$
Nilai ini mencerminkan keseimbangan performa model dalam mengenali penderita diabetes sekaligus menghindari kesalahan klasifikasi positif yang berlebihan. Secara keseluruhan, model menunjukkan performa yang sangat baik, meskipun sensitivitas terhadap kasus diabetes masih dapat ditingkatkan. Untuk memahami lebih lanjut bagaimana model membuat prediksi, dilakukan analisis terhadap pentingnya fitur dan kontribusinya terhadap output model.

1. Feature Importance – XGBoost
    ![Gambar 11. Feature Importance](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-10.png?raw=true)
    Hasil feature importance dari model XGBoost menunjukkan bahwa HbA1c level merupakan prediktor paling dominan dengan skor penting sekitar 0,53, diikuti oleh blood glucose level sebesar 0,32. Kedua variabel ini merupakan indikator klinis utama dalam diagnosis diabetes, sehingga konsistensi ini memperkuat validitas model. Fitur-fitur lain seperti age, hypertension, dan heart_disease menunjukkan kontribusi yang jauh lebih kecil (masing-masing <0,05), menandakan bahwa meskipun relevan secara klinis, pengaruhnya dalam model prediktif lebih rendah. BMI, gender, dan smoking_history memiliki nilai penting yang sangat rendah (<0,03), menunjukkan peran minimal dalam klasifikasi oleh model ini. Namun, analisis ini hanya menggambarkan pengaruh secara agregat; untuk mengevaluasi kontribusi fitur pada tingkat individual, digunakan pendekatan berbasis SHAP.

2. SHAP Summary Plot
    ![Gambar 12. SHAP Summary](https://github.com/Alqurtubi17/mlt-klasifikasi/blob/master/image-11.png?raw=true)
    Visualisasi nilai SHAP (SHapley Additive exPlanations) memperlihatkan dampak setiap fitur terhadap output prediksi baik secara individual maupun global. HbA1c level dan blood glucose level tidak hanya dominan dalam feature importance, tetapi juga memiliki SHAP value yang tinggi dan terdistribusi luas, baik ke arah positif maupun negatif, menunjukkan bahwa nilai tinggi dari kedua fitur ini secara konsisten mendorong prediksi ke arah diabetes. Fitur age dan BMI juga berkontribusi secara signifikan, dengan nilai tinggi yang meningkatkan probabilitas klasifikasi positif terhadap diabetes, meskipun dengan magnitudo yang lebih rendah dibanding HbA1c. Sementara itu, fitur seperti gender, heart_disease, hypertension, dan smoking_history menunjukkan distribusi SHAP yang lebih sempit dan kecil, mencerminkan dampak yang terbatas terhadap keputusan model. Analisis SHAP ini memperkuat hasil feature importance sebelumnya dan memberikan wawasan lebih dalam mengenai interpretabilitas model secara lokal dan global.

### Kesimpulan
---
Berdasarkan seluruh proses analisis dan eksperimen yang telah dilakukan, berikut adalah kesimpulan yang menjawab pertanyaan penelitian dan tujuan dari proyek ini:

1. Fitur yang Paling Berpengaruh terhadap Prediksi Risiko Diabetes

    Hasil analisis feature importance dari model XGBoost dan interpretasi berbasis SHAP (SHapley Additive exPlanations) menunjukkan bahwa fitur HbA1c level dan blood glucose level merupakan dua fitur paling berpengaruh dalam memprediksi risiko diabetes. Kedua fitur ini secara klinis memang dikenal sebagai indikator utama diagnosis diabetes, dan model pun menempatkannya sebagai penentu dominan dalam klasifikasi. Fitur lain seperti age dan BMI juga memberikan kontribusi yang cukup signifikan, sementara fitur seperti gender, heart_disease, hypertension, dan smoking_history memiliki dampak yang relatif kecil terhadap output model.

2. Algoritma Machine Learning Paling Efektif
    
    Dari tiga algoritma yang diuji – Random Forest, XGBoost, dan Logistic Regression – hasil evaluasi menunjukkan bahwa XGBoost merupakan model dengan performa terbaik secara keseluruhan. Meskipun Random Forest memiliki akurasi tinggi (±94.9%), XGBoost unggul dalam F1 Score dan Precision, yang sangat penting dalam konteks prediksi medis, terutama untuk menghindari kesalahan klasifikasi positif palsu (false positives) atau negatif palsu (false negatives). Model XGBoost mencatat nilai F1 Score sebesar 0.79, dengan Precision 0.89, dan Akurasi 96%, menjadikannya pilihan utama sebagai model final.

3. Tujuan Proyek Tercapai
    
    - Model prediktif yang dikembangkan berhasil mengklasifikasikan individu berisiko diabetes dengan akurasi tinggi, serta metrik evaluasi yang memadai. 
    - Tiga algoritma klasifikasi telah dibandingkan secara adil dengan proses hyperparameter tuning, dan XGBoost dipilih sebagai model terbaik berdasarkan performa metrik evaluasi yang komprehensif.
    - Analisis pentingnya fitur dengan pendekatan feature importance dan SHAP telah mengidentifikasi fitur-fitur kunci yang berkontribusi besar terhadap prediksi, sehingga dapat menjadi referensi penting dalam pengambilan keputusan klinis.

## **Referensi**
- Apriliah, W., Kurniawan, I., Baydhowi, M., & Haryati, T. (2021). SISTEMASI: Jurnal Sistem Informasi Prediksi Kemungkinan Diabetes pada Tahap Awal Menggunakan Algoritma Klasifikasi Random Forest (Vol. 10, Issue 1). 
- Hasanzad, M., Larijani, B., & Aghaei Meybodi, H. R. (2022). Diabetes and COVID-19: a bitter nightmare. Journal of Diabetes and Metabolic Disorders, 10–12. https://doi.org/10.1007/s40200-02200994-5.
- Hovi, H. S. W., Id Hadiana, A., & Rakhmat Umbara, F. (2022). Prediksi Penyakit Diabetes Menggunakan Algoritma Support Vector 
Machine (SVM). Informatics and Digital Expert (INDEX), 4(1), 40–45. https://doi.org/10.36423/index.v4i1.895.
- Saputro, K. A., Atsir, E. M., & Hasanah, H. (2024).Perbandingan Tingkat Akurasi Penyakit Diabetes Menggunakan Metode Regresi Logistik dan Random Forest. TAMIKA: Jurnal Tugas Akhir Manajemen Informatika & Komputerisasi Akuntansi, 4(2), 159-166.
- Widodo, A. M., Anggraeni, Y. S., Anwar, N., Ichwani, A., & Sekti, B. A. (2021). Performansi K-NN, J48, Naive Bayes dan Regresi Logistik sebagai Algoritma Pengklasifikasi Diabetes.  Prosiding SISFOTEK, 27–33. 
- Yusnita, Y., Djafar, M. H. A., & Tuharea, R. (2021). Risiko Gejala Komplikasi Diabetes Mellitus Tipe II di UPTD Diabetes Center Kota Ternate. Media Publikasi Promosi Kesehatan Indonesia (MPPKI), 4(1), 60–73. 
