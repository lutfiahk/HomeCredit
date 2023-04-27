# Client Payment Prediction 
## with CLASSIFICATION MODELING

![image.png](https://awsimages.detik.net.id/visual/2018/02/06/e71aa604-07f0-40e6-92d6-c65938849fc8_169.jpeg?w=715&q=90)

Problem statement :<br>
PT. HOME CREDIT merupakan suatu perusahaan perusahaan pembiayaan multiguna multinasional yang memberikan layanan pembiayaan bagi pelanggan. Terdapat banyak pengajuan credit yang masuk tetapi akan sangat menghabiskan banyak waktu jika harus dilakukan review pengajuan satu per satu secara manual. <br>
Business Metric :<br>
Banyak pengajuan credit yang dapat direview per harinya.<br>
Solution : <br>
Dibuat suatu model yang dapat melakukan prediksi client payment secara otomatis yang dapat digunakan untuk mempermudah mengambil keputusan penerimaan pengajuan credit.<br>
Model prediksi ini menggunakan Model Klasifikasi dengan algoritma Logistic Regression, Decision Tree, XGBoost, dan Random Forest yang kemudian akan dibandingkan untuk melihat model mana yang memiliki performa paling baik untuk melakukan prediksi.
<br><br>
Dataset yang digunakan dapat diakses di : https://drive.google.com/file/d/1qZa4C5KuaWC04UB7puVxMC5vyt5m4S5j/view?usp=sharing<br>
<br>
Data yang digunakan merupakan data profil client, dimana pada project ini hanya akan digunakan feature :
| Column              | Description                                 |
| ------------------- | ------------------------------------------- |
| SK_ID_CURR          | ID client                                   |
| TARGET              | LABEL TARGET yang akan diprediksi           |
| NAME_CONTRACT_TYPE  | Nama tipe kontrak                           |
| CODE_GENDER         | Gender                                      |
| FLAG_OWN_CAR        | Kepemilikan mobil (Ya/Y, atau Tidak/N)      |
| FLAG_OWN_REALTY     | Kepemilikan Properti (Ya/Y, atau Tidak/N)   |
| CNT_CHILDREN        | Banyak anak                                 |
| AMT_INCOME_TOTAL    | Total Pemasukan                             |
| AMT_CREDIT          | Total Kredit                                |
| AMT_ANNUITY         | Total Anuitas                               |
| AMT_GOODS_PRICE     | Total harga rumah yang dikreditkan          |
| NAME_INCOME_TYPE    | Tipe pemasukan                              |
| NAME_EDUCATION_TYPE | Pendidikan                                  |
| NAME_FAMILY_STATUS  | Status keluarga                             |
| CNT_FAM_MEMBERS     | Banyak anggota keluarga                     |
<br>
<b>Role<\b> ‘model klasifikasi’ dalam project ini adalah melakukan prediksi client payment dengan memberikan :
<b>Label 1<\b> untuk client yang dianggap akan melakukan gagal bayar
<b>Label  0<\b> untuk client yang dianggap tidak akan melakukan gagal bayar

### Step by Step
* Data Cleansing <br>
Dilakukan Cleansing data dari missing value, duplicated data, dan data yang tidak sesuai.
<br> 
* Data Preprocessing<br>
Kemudian dilakukan data preprocessing dengan melakukan data splitting, outlier handling, feature encoding dan transformation, kemudian dilakukan imbalance class handling dengan SMOTE method.
<br>
* Data Modeling<br>
Dilakukan modeling prediksi dengan beberapa algoritma, dimana diperoleh :<br>
| Model                  | Accuracy and Recall Score                          |
| ---------------------- | -------------------------------------------------- |
| Logistic regression    | Accuracy (Test Set): 0.67, Recall (Test Set): 0.43 |
| Decision Tree          | Accuracy (Test Set): 0.41, Recall (Test Set): 0.62 |
| XGBoost                | Accuracy (Test Set): 0.25, Recall (Test Set): 0.83 |
| Random Forest          | Accuracy (Test Set): 0.61, Recall (Test Set): 0.46 |
<br>
Dari empat model yang digunakan, diketahui metode/model dengan nilai akurasi paling tinggi adalah model <b>Logistic Regression<\b>. Tetapi selain dengan melihat nilai akurasinya, kami juga mengutamakan untuk mempertimbangkan nilai <b>recall<\b>, karena tujuan utama dari model ini adalah berfokus untuk mengurangi false negative atau dalam kasus ini adalah client yang salah diprediksi tidak akan gagal bayar. Dan model dengan nilai recall tertinggi adalah XGBoost.
<br>
Tetapi untuk model XGBoost, nilai akurasi sangat buruk, yaitu hanya 24%, sehingga kami pertimbangkan akan lebih robust jika menggunakan <b>Logistic regression<\b>.
<br>
Untuk meningkatkan performa model, akan dilakukan hyperparameter tuning dengan parameter Regularization Parameter (C), dan penalty dengan 'L2'. <br>
<b>Diperoleh hasil :<\b><br>
<b> Confusion Matrix<\b><br>
|               | 0 (predicted) | 1 (predicted) |
| ------------- | ------------- | ------------- |
| 0 (actual)    | 45757         | 38935         |
| 1 (actual)    | 2822          | 4652          |

<br><b>Performance Score:<\b>		 <br>
Accuracy (Test Set): 0.55
Recall (Test Set): 0.62
roc_auc (train-proba): 0.63
roc_auc (test-proba): 0.62
<br>
Setelah melakukan hyperparameter tuning, diketahui nilai recall model Logisticregression naik dari 47% menjadi 63%. Dan client yang tepat diprediksi akan gagal bayar bertambah, hal ini akan sangat menguntungkan karena kita dapat dengan mudah mengidentifikasi mana client yang akan gagal bayar di masa depan.
<br>
Dari **Feature Importance Plot** di bawah ini diketahui nilai AMT_CREDIT memiliki korelasi positif yang tinggi terhadap label target, hal ini mengindikasikan semakin tinggi nilai total kredit miliki client maka diprediksi bahwa client cenderung akan mengalami gagal bayar. Feature AMT_GOODS_PRICE memiliki nilai korelasi negatif yang tinggi, hal ini mengindikasikan bahwa semakin rendah nilai harga barang yang diajukan untuk dikreditkan, maka client akan semakin bertendensi untuk mengalami gagal bayar di masa depan.
<br>![Alt text](https://github.com/lutfiahusnakhoirunnisa/HomeCredit/blob/main/Feature%20Importance%20Plot.png)<br>
<br>
* Implementation<br>
Untuk melihat bagaimana impact dari model, dilakukan Simulasi penggunaan model dengan menggunakan data test, dimana pada data test diketahui terdapat 7474 client yang mengalami masalah pembayaran.
Jika diasumsikan sebelum adanya model, bank melakukan review pengajuain kredit client secara manual, maka perusahaan perlu melakukan review 7474 pengajuan credit client.
Jika menggunakan model ini, perusahaan dapat melihat bagaimana prediksi label targetnya, dan cukup perlu melakukan review lanjutan pada client yang diprediksi akan mengalami gagal bayar. Dimana pada data test, diprediksi sebanyak 43587 client akan gagal bayar, atau kurang lebih hanya separuh dari total client awal.
<br>
Kemudian disumsikan telah dilakukan review lanjutan, dan client yang tepat diprediksi akan gagal bayar akan ditolak pengajuan kreditnya. Diperoleh :
Persentase client gagal bayar awal :  0.081
Total semua client awal :  92166
Persentase client gagal bayar setelah penerapan model :  0.032
Total client yang diapprove kreditnya :  87514
<br>
Persentase client yang gagal bayar dapat turun dari 8% menjadi 3%, dengan banyak client yang diapprove turun dari 92.166 menjadi hanya 87.514
<br>
### Conclusion and Business Recommendation
* Dari model yang digunakan, Logistic regression memiliki performa paling baik. Selanjutnya model ini sebaiknya digunakan untuk melakukan prediksi client yang gagal bayar di masa depan sehingga review pengajuan kredit client dapat dilakukan dengan lebih mudah dan lebih cepat. 
* Performa model dianggap baik, tapi masih kurang akurat. Selanjutnya mungkin harus dilakukan pemilihan feature yang lebih merepresentasikan customer dengan baik, dan mudah dilakukan maintenancenya sehingga model dapat digunakan secara berlanjut. Model dengan algoritma lain mungkin dapat diexplore lebih lanjut untuk menemukan model dengan performa lebih tinggi.
* Melakukan review lanjutan secara manual pasti memerlukan waktu, dan cost, dimana sumber daya tersebut terbatas. Sehingga kita perlu menerapkan client prioritas yang perlu direview lebih lanjut. Hal ini dapat dilakukan dengan melihat total kredit dan harga barang yang diajukan untuk kredit, karena dua feature ini memiliki nilai koefisien feature importance yang tinggi.
* Untuk menentukan customer prioritas yang harus direview, akan lebih mudah jika dilakukan client credit scoring daripada harus melihat nilai total kredit dan harga barang secara mentah. Direkomendasikan untuk membuat model baru untuk melakukan credit scoring ini
