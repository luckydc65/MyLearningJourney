# Introduction
## Overal Goal
Kamu seorang marketing analyst dan kamu diminta oleh Chief Marketing Officer bahwa marketing campaigns saat ini tidak seefektif yang mereka bayangkan. Kamu butuh untuk menganalisis data untuk mengerti masalah ini dan memberikan solusi berdasarkan data.

## Section 01: Exploratory Data Analysis
1. Apakah terdapat missing value atau outliers? Bagaimana kamu akan mengatasinya? <br />
2. Apakah terdapat variabel berguna yang dapat direkayasa dengan data yang diberikan? <br />
3. Apakah kamu melihat ada pola atau anomali di data? <br />

## Section 02: Statistical Analysis
1. Faktor-faktor apa yang secara signifikan berhubungan dengan jumlah pembelian toko?
2. Apakah tarif US jauh lebih baik dibandingkan negara lain di Dunia dalam hal total pembelian?
3. Supervisor anda  bersikeras bahwa orang yang membeli emas lebih konservatif. Oleh karena itu, orang yang menghabiskan jumlah emas diatas rata-rata dalam 2 tahun terakhir, lebih banyak melakukan pembelian di toko. Membenarkan atau sangkal pernyataan ini menggunakan uji statistika yang sesuai.
4. Ikan terdapat asam lemak Omega 3 yang bagus untuk otak. Dengan demikian, apakah “Married PhD candidates” memiliki hubungan yang signifikan dengan jumlah yang dihabiskan untuk ikan?
5. Apakah terdapat hunungan signifikan antara wilayah geografis dan keberhasilan dari campaign?

## Section 03: Data Visualization
Silahkan plot dan visualisasikan jawaban dari pertanyaan dibawah ini.
1. Marketing campaign mana yang paling berhasil?
2. Seperti apa rata-rata pelanggan untuk perusahaan ini?
3. Produk mana yang memiliki performa terbaik?
4. Channels mana yang memiliki performa buruk?

# Section 01: Exploratory Data Analysis
## 1. Apakah terdapat missing value atau outliers? Bagaimana kamu akan mengatasinya?
Berdasarkan pengamatan pada data, terdapat missing value pada kolom Income sebanyak 24 missing value.
Akan dilihat distribusi dari kolom income tersebut untuk menentukan strategi terbaik untuk melakukan imputasi pada missing value. <br /> <br />
![image](https://user-images.githubusercontent.com/80409975/149909371-0bd19764-0a50-4206-afab-46a72d9e7467.png) <br /> <br />

![image](https://user-images.githubusercontent.com/80409975/149909473-d9751412-e643-438f-880b-f6ba305b7011.png) <br /> <br />

Kebanyakan income terdistribusi diantara 1.730-108.120 dengan beberapa outliers. Missing value akan diimput dengan nilai median, untuk menghindari efek dari outliers dalam pengimputan nilai. <br /> <br />

![image](https://user-images.githubusercontent.com/80409975/149909869-7fd4b060-a4d7-4b73-bb84-adc2b5a2b134.png)  <br /> <br />

Dari hasil pengamatan, terdapat outliers dimana ada 3 customer dengan kelahiran pada tahun < 1900, yang dimana apabila dihitung berusia > 110 tahun ketika melakukan Enrollment.
Customer dengan tahun kelahiran <1900 akan kita remove

## 2. Apakah terdapat variabel berguna yang dapat direkayasa dengan data yang diberikan?
1. Jumlah total dari tanggungan di rumah (‘Dependents’) dapat direkayasa dengan menjumlahkan ‘Kidhome’ dan ‘Teenhome’
2. Tahun menjadi customer (‘Year_Enroll’) dapat direkayasa dari ‘Dt_Customer’
3. Usia saat menjadi customer (‘Age_Enroll’) dapat direkayasa dengan mengurangkan ‘Year_Enroll’ dengan ‘Year_Birth’
4. Total yang dibelanjakan (‘TotalMnt’) dapat direkayasa dengan menjumlahkan semua fiture yang mengandung keyword ‘Mnt’
5. Total Pembelian (‘TotalPurchases’) dapat direkayasa dengan menjumlahkan semua fitur yang mengandung keyword ‘Purchases’
6. Jumlah total campaigns yang diterima (‘TotalCampaignsAcc’) dapat direkayasa dengan menjumlahkan semua fitur yang mengandung keywords ‘Cmp’ dan ‘Response’ (Campaign terakhir)

# 3. Apakah ada pola atau anomali di data?
![image](https://user-images.githubusercontent.com/80409975/149910349-c8caa008-eaaa-4e2f-98d2-117ec60872fe.png)

Jumlah yang dibelanjakan (‘Total Amount’ dan fitur "Amount" lainnya) berkorelasi positif dengan "Income". Pembelian di toko, di web, atau melalui katalog berkorelasi positif dengan "Income" <br /> <br /> <br />

![image](https://user-images.githubusercontent.com/80409975/149910426-589cc804-c44d-49e6-826a-f500da263cb1.png) <br /> <br />
Jumlah yang dibelanjakan (‘Total Amount Spent’ dan fitur ‘Amount’ lainnya) dan jumlah pembelian (‘Total Purchases’ dan fitur ‘Purchases with ...’ lainnya) berkorelasi negatif dengan orang yang memiliki tanggungan dirumah (‘Dependents’). Pembelian dengan diskon berkorelasi positif dengan orang yang memiliki tanggungan dirumah (‘Dependents’).

![image](https://user-images.githubusercontent.com/80409975/149910661-9fd731ac-d201-4d65-81ca-38c045b45b10.png)
![image](https://user-images.githubusercontent.com/80409975/149910676-047efff6-6c34-440b-b734-92df0ef72988.png) <br /> <br />
Jumlah dari kunjungan pada web tidak berkorelasi positif dengan jumlah pembelian di web <br /> <br />

![image](https://user-images.githubusercontent.com/80409975/149910910-c305061c-c168-4709-979b-7eb8396e2887.png)
![image](https://user-images.githubusercontent.com/80409975/149910941-b242fd3f-9015-4aa8-b915-caf057891959.png) <br /> <br />
Akan tetapi, jumlah kunjungan pada website berkorelasi positif dengan jumlah pembelian dengan diskon, menunjukan bahwa diskon adalah cara yang efektif untuk memancing orang dalam melakukan pembelian diwebsite.

### Efek dari memiliki tanggungan (anak-anak & remaja) terhadap jumlah uang yang dibelanjakan
![image](https://user-images.githubusercontent.com/80409975/149911448-b786ec45-b4c1-4105-8125-62c487543954.png) <br /> <br />
Dari gambar disamping, orang yang memiliki tanggungan yang lebih banyak, jumlah uang yang dibelanjakan akan semakin sedikit.

### Efek memiliki tanggungan (Anak-anak & Remaja) dalam jumlah pembelian dengan diskon
![image](https://user-images.githubusercontent.com/80409975/149911602-d31a1bbe-1468-4755-a41a-fa378870dee2.png) <br /> <br />
Dari gambar disamping, orang yang memiliki tanggungan lebih banyak, jumlah pembelian dengan diskon lebih banyak juga.

### Efek dari pada penerimaan campaign
![image](https://user-images.githubusercontent.com/80409975/149911706-c7ef7160-fc68-4b05-9b57-11275c570072.png) <br /> <br />
Orang dengan pendapatan lebih besar lebih banyak dalam menerima kampanye iklan dibandingkan dengan yang berpendapatan lebih kecil.

### Efek dari memiliki tanggungan (Anak-anak & Remaja) pada penerimaan campaign
![image](https://user-images.githubusercontent.com/80409975/149911809-9f31a8eb-a948-4864-97d4-09d6a2224485.png) <br /> <br />
Semakin banyak tanggungan yang dimiliki, semakin sedikit kampanye iklan yang diterima.

# Section 02: Statistical Analysis
## 1. Faktor-faktor apa yang secara signifikan berhubungan dengan jumlah pembelian di toko?
![image](https://user-images.githubusercontent.com/80409975/149912234-bee64a00-8812-4327-a797-5f9124a43a74.png)  <br /> <br />
Faktor yang berhubungan dengan jumlah pembelian di toko yaitu:
1. jumlah yang dihabiskan untuk Wine, Pendapatan, dan pembelian dengan katalog (Berkorelasi Positif)
2. Memiliki anak kecil dan kunjungan di web (Berkorelasi Negatif)

## 2. Apakah tarif US jauh lebih baik dibandingkan negara lain di Dunia dalam hal total pembelian?
![image](https://user-images.githubusercontent.com/80409975/149912774-de424c48-3680-4bb3-ae70-3e174a1bb743.png) <br /> <br />
Spain (SP) memperoleh jumlah terbanyak dalam hal total pembelian. Sedangkan US merupakan negara kedua terakhir dalam hal total pembelian.

## 3. Apakah orang yang menghabiskan jumlah emas diatas rata-rata dalam 2 tahun terakhir, lebih banyak melakukan pembelian di toko?
![image](https://user-images.githubusercontent.com/80409975/149913088-38ef526c-134f-4539-98aa-1650d8c2a7b3.png) <br /> <br />
Orang yang menghabiskan jumlah emas diatas rata-rata lebih banyak melakukan pembelian di toko dibandingkan dengan yang dibawah rata-rata.

## 4. Apakah “Married PhD candidates” memiliki hubungan yang signifikan dengan jumlah yang dihabiskan untuk ikan? 
![image](https://user-images.githubusercontent.com/80409975/149913361-10d80558-c8c0-4139-95d0-6c655b83402d.png) <br/ > <br />
Married PhD candidates menghabiskan lebih sedikit di produk ikan dibandingkan dengan customer lainnya. 

### Faktor apa yang sangat berhubungan dengan jumlah yang dihabiskan untuk produk ikan?
![image](https://user-images.githubusercontent.com/80409975/149913542-4b49332f-f93d-49ef-baff-6331eff6d766.png) <br/ > <br />
Faktor yang berhubungan dengan jumlah yang dihabiskan untuk produk ikan :
1. Jumlah yang dihabiskan untuk Buah, Jumlah yang dihabiskan untuk Permen, Jumlah yang dihabiskan untuk Daging, Pembelian di Katalog, dan Pendapatan  (Berkorelasi Positif)
2. Kunjungan di web dan Memiliki anak kecil (Berkorelasi Negatif)















