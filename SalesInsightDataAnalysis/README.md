Pada project kali ini saya akan menuliskan yang saya pelajari dari channel youtube *"codebasics"*, pada project ini aplikasi yang digunakan yaitu **Power BI**, dataset yang digunakan diambil dari https://github.com/codebasics/DataAnalysisProjects
# Import Dataset
## 1. Import ke MYSQL Workbench
Dataset yang digunakan menggunakan format **.sql**, maka pertama saya akan mengimport dataset tersebut ke aplikasi **MYSQL Workbench** dengan langkah sebagai berikut: <br />
1. Klik **Server > Data Import** maka akan muncul tampilan sebagai berikut <br />
![Capture](https://user-images.githubusercontent.com/80409975/140283732-735eecf2-4bd1-45c8-9fe9-bc567eb1bec7.JPG)
2. Kemudian klik **Import from Self-Contained File** dan kemudian pilih file dataset yang ingin dimasukan <br />
![Capture1](https://user-images.githubusercontent.com/80409975/140284195-9c72246b-f69e-4fa0-985a-5985441ac45e.JPG) <br /> <br />
3. Kemudian klik **Start Import**
4. Maka dataset akan tersedia pada bagian **SCHEMAS** <br /> <br />
 ![Capture3](https://user-images.githubusercontent.com/80409975/140284640-0cef5311-bbae-408e-a567-f0146597ac24.JPG)
 
 ## 2. Import ke Power BI
 Pada tahap ini kita akan import dataset tersebut ke **Power BI** untuk kemudian diolah, langkah yang dilakukan adalah sebagai berikut:
 1. Pilih **Home > Get Data> More...** <br /> ![PowerBI](https://user-images.githubusercontent.com/80409975/140285830-a9fe9e18-7330-4fe8-a084-5b4ae0e0f2a2.JPG)<br /><br />
 2. Setelah itu akan muncul jendela sebagai berikut, kemudian klik **Database > MYSql database** <br /> ![Power BI2](https://user-images.githubusercontent.com/80409975/140286687-f5afb8d5-7ed5-4f80-9ad7-659cb1a38b44.JPG)<br /> <br />
 3. Kemudian untuk **Server** diisi dengan *localhost*, dan **Database** diisi dengan nama dari database, untuk kasus ini isi dengan *sales*, kemudian klik **OK**
 4. Setelah itu akan muncul jendela sebagai berikut, dan berikan tanda checklist pada semua data <br /> ![Power BI3](https://user-images.githubusercontent.com/80409975/140287704-7d5f8e61-ee63-4883-a18b-ab1ae9ef168e.JPG)<br /> <br />
 5. Terakhir klik **Load** sehingga dataset siap untuk digunakan
 
 # Data Cleaning
Pada tahap ini akan dilakukan proses pembersihan data untuk melakukannya di Power BI. <br />
Pertama saya akan membuat relasi antar Table dengan attribute yang sama yaitu, *markets_code* yang ada pada tabel **sales markets** dihubungkan dengan *markets_code* yang ada pada tabel **sales transactions**, kemudian *date* yang ada pada tabel **sales date** dihubungkan dengan *order_date* pada **sales transactions**.  <br /> 
![Power BI4](https://user-images.githubusercontent.com/80409975/140291647-6ed1f676-3926-45e1-a2d2-41c56718fa44.JPG) <br /> <br /> 
Setelah dibuat relasi antar tabel selanjutnya lakukan pembersihan data yang dapat dilakukan dengan klik **Home > Transform Data**, cara menggunakan Power BI mirip dengan Microsoft Excel. <br /> <br />
Saat melihat bagian *sales markets* pada *markets_name* terdapat record *new york* dan *paris*, karena pada kasus ini kita hanya akan berfokus pada transaksi yang dilakukan di India, maka kedua record tersebut akan kita hilangkan dengan memfilter data. <br />
![Power BI5](https://user-images.githubusercontent.com/80409975/140293338-c4156cbe-b227-4e3d-9242-182654719468.JPG) <br /> <br />
dan <br />
![Power BI6](https://user-images.githubusercontent.com/80409975/140293583-6773601b-3da1-4dbf-8a4d-0a1603c56c16.JPG) <br /> <br />
Kita lihat lagi dibagian **sales transactions** terdapat duplicate data untuk attribute *currency* dengan record USD karena memiliki kesamaan pada *order_date*, *sales_qty*, dan *sales_amount* sehingga harus kita hapus duplicate data tersebut dengan hanya menggunakan **currency = "USD#(cr)"** (terdapat dua jenis USD yaitu, dua record "USD" dan dua record "USD#(cr)") . <br />
![Power BI7](https://user-images.githubusercontent.com/80409975/140294729-a4289487-65c2-4ea8-a048-765f21472964.JPG) <br /> <br />
Setelah mengecek untuk *currency* USD kemudian kemudian lihat juga pada *currency* INR. Pada *currency* INR juga terdapat dua jenis yaitu, "INR" dan "INR#(cr)". Saat dicek dengan menggunakan MYSql terdapat 150.000 record untuk "INR#(cr)" dan 279 record untuk "INR". Langkah pertama yang saya lakukan yaitu melihat record pada "INR" dan kemudian urutkan berdasarkan *sales_amount* terbesar dengan beberapa nilai seperti berikut 170185,143560,126296,107500 dan 105301. Setelah mendapatkan beberapa nilai terbesar tersebut kemudian cek untuk kedua jenis INR tersebut ("INR" dan "INR#(cr)") yang hanya menampilkan beberapa nilai terbesar tersebut. <br />
![Power BI8](https://user-images.githubusercontent.com/80409975/140303325-b2433fe5-fad2-4eba-90f2-7f569f1b954f.JPG) <br /> <br />
Dari gambar tersebut juga terlihat terjadinya duplicate sehingga untuk kasus ini hanya akan digunakan *currency* "USD#(cr)" dan "INR#(cr)". Pada *sales_amount* terdapat nilai -1 dan 0, oleh karena itu filter data yang tidak ada nilai -1 dan 0. Langkah selanjutnya yang akan dilakukan adalah menormalisasi nilai *sales_amount* dengan *currency* "USD" disesuaikan dengan "INR" (Indian Rupee) dengan menambahkan kolom *norm_sales_amount*, pilih Add **Column > Custom Column** dan masukan syntax sebagai berikut dan klik **ok**. <br />
![Power BI9](https://user-images.githubusercontent.com/80409975/140308255-f9ebbcb3-9512-4a92-a7fb-d9338eac9db0.JPG) <br /> <br />
<br />
Setelah muncul kolom *norm_sales_amount* ubah tipe data tersebut dengan klik **Transform > Data type:Any** ubah menjadi **Decimal Number**. Setelah data dibersihkan kemudian simpan data tersebut dengan klik **Home > Close&Aplly**. <br />

## Build Dashboard
Pada tahap ini akan ditunjukan langkah-langkah yang dilakukan untuk membuat dashboard pada Power BI. Pertama-tama kita akan menambahkan data *revenue* untuk menghitung total pendapatan dari perusahaan. Cara menambahkannya dengan klik **Home > Enter data** kemudian berikan nama Tabel dengan *Base Measures* dan klik **load**. Setelah Tabel dibuat kemudian kita buat *measure* pada tabel tersebut dengan cara klik titik tiga di samping *BaseMeasures* <br />
![bi](https://user-images.githubusercontent.com/80409975/140469758-a9b40d01-e27a-45e4-bc0e-4812c96e9fc8.JPG) <br />
Langkah selanjutnya adalah klik **New measure** dan isikan measure tersebut dengan syntax. <br /> **revenue = SUM('sales transactions'[norm_sales_amount])** <br />
Beberapa measure yang perlu dibuat diantaranya *Total Sales*, *Total cost*, *Total profit*, dan *Profit Margin* dengan syntax sebagai berikut: <br />
**Total Sales = SUM('sales transactions'[sales_qty])** <br /> 
**Total Cost = SUM('sales transactions'[cost_price])** <br /> 
**Total Profit = SUM('sales transactions'[Profit])** <br />
**Profit Margin = [Total Profit]/[Revenue]** <br />
Setelah measure terbuat selanjutnya buat dashboard dengan cara pindahkan measure revenue (dragging) kemudian letakan pada lembar dashboard (dropping) seperti pada gambar. <br /> 
![bi2](https://user-images.githubusercontent.com/80409975/140487082-3a54c9c9-1452-487c-a774-44918664647b.JPG) <br />  <br /> 
Kemudian dapat disesuaikan bentuk dari visualisasinya dengan memilih pada **Visualizations** untuk revenue akan digunakan jenis card. <br /> <br /> 
![bi3](https://user-images.githubusercontent.com/80409975/140489124-b2042518-c1f0-4d78-873b-d8e0c6e3f2de.JPG) <br /> <br /> 
Berikut ini merupakan hasil dari dashboard yang sudah dibuat dengan analisis berdasar revenue. <br />
![image](https://user-images.githubusercontent.com/80409975/140749917-1bbf5d14-f743-4d0f-87ac-3722bbb7c6a4.png) <br /> <br />
Kemudian dashboard berikut ini merupakan analisis berdasarkan profit. <br /> <br />
![image](https://user-images.githubusercontent.com/80409975/140749760-801b672c-2d41-4d90-9d3d-b24c9d705621.png)

