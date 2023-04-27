# Client Payment Prediction 
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

### Step by Step
* Data Cleansing and Preprocessing<br>
Dilakukan 
<br> 
<br><br><br>
<br><br>
<br>
<br>
<br>
### Business Recommendation
Conclusion :
* Dari model yang digunakan, Logistic regression memiliki performa paling baik. Selanjutnya model ini sebaiknya digunakan untuk melakukan prediksi client yang gagal bayar di masa depan sehingga review pengajuan kredit client dapat dilakukan dengan lebih mudah dan lebih cepat. 
* Performa model dianggap baik, tapi masih kurang akurat. Selanjutnya mungkin harus dilakukan pemilihan feature yang lebih merepresentasikan customer dengan baik, dan mudah dilakukan maintenancenya sehingga model dapat digunakan secara berlanjut. Model dengan algoritma lain mungkin dapat diexplore lebih lanjut untuk menemukan model dengan performa lebih tinggi.
* Melakukan review lanjutan secara manual pasti memerlukan waktu, dan cost, dimana sumber daya tersebut terbatas. Sehingga kita perlu menerapkan client prioritas yang perlu direview lebih lanjut. Hal ini dapat dilakukan dengan melihat total kredit dan harga barang yang diajukan untuk kredit, karena dua feature ini memiliki nilai koefisien feature importance yang tinggi.
* Untuk menentukan customer prioritas yang harus direview, akan lebih mudah jika dilakukan client credit scoring daripada harus melihat nilai total kredit dan harga barang secara mentah. Direkomendasikan untuk membuat model baru untuk melakukan credit scoring ini
