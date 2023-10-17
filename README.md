Credit Card Customer Segmentation Analysis
====================================

Collaborators
------------
1. [Ihza Yusuf Amirul Umam](https://github.com/ihzayusuf29)
2. [Fajar Dwi Kurnianto](https://github.com/fdkurnianto)
3. [Faisal Nur Khairudin](https://github.com/fnkhairudin)

Context
------------
Terdapat suatu perusahaan yang bergerak dibidang perbankan/keuangan, yaitu Bank Beta. Saat ini Bank Beta memiliki suatu data mengenai perilaku kurang lebih 9000 pengguna/nasabah yang menggunakan kartu kredit selama 6 bulan kebelakang. Beberapa perilaku tersebut antara lain, jumlah sisa saldo yang dapat digunakan (balance), seberapa sering nasabah menggunakan kartu kreditnya, jumlah saldo yang telah digunakan, dll.

Problem Statement
------------
Saat ini Marketing Departement masih kesulitan untuk mengadakan campaign marketing kepada para nasabahnya, karena masih belum mengetahui karakteristik dari para nasabahnya. Campaign marketing yang tepat sangat penting untuk dilakukan, berdasarkan referensi di bawah, jika melakukan campaign marketing yang tidak tepat sasaran dan nasabah memiliki pengalaman yang buruk (negative experiences) hanya satu kali saja, sehingga gagal untuk memenuhi ekspektasi dari nasabah, maka 61% dari total nasabah akan pindah ke competitor lainnya. Bahkan, akan meninggkat menjadi 76% jika nasabah memiliki pengalaman yang buruk (negative experiences) hingga berkali-kali. Jika hal ini terjadi pada Bank Beta, tentu hal ini akan berdampak buruk bagi revenue Bank Beta. Selain itu, rata-rata per tahun bank kehilangan nasabahnya sebesar 12.5%, sedangkan akuisisi nasabah baru sebesar 13%, namun biaya (cost) akuisisi nasabah baru 5 kali lebih besar daripada mempertahankan nasabah lama. Kemudian, jika ada pengurangan 5% (saja) dari nasabah yang hilang (customer turnover), maka bank bisa meningkatkan net profit sebesar 80%. Oleh karena itu, Bank Beta ingin meminimalisir kemungkinan hal tersebut terjadi. Salah satu cara yang dapat dilakukan adalah dengan melakukan campaign marketing yang tepat ke nasabah yang tepat pula.
Tim Data Scientist akan merumuskan beberapa permasalahan, antara lain:
- Bagaimana pola-pola (pattern)/karakteristik tersembunyi dari para nasabah jika dilakukan pendekatan menggunakan algoritma unsupervised machine larning ?
- Bagaimana karakteristik dari masing-masing cluster terbentuk ?

Goals
------------
Bank Beta bisa mengetahui bagaimana karakteristik para nasabah. Dengan mengetahui karakteristik tersebut, tim Marketing Departement Bank Beta bisa melakukan campaign marketing yang tepat untuk para nasabahnya. Diharapkan dengan campaign marketing yang tepat dapat membuat para nasabah untuk semakin sering menggunakan kartu kreditnya, sehingga Bank beta dapat meningkatkan revenue.

Project Stakeholders
------------
Marketing Departement: departement ini bertanggungjawab untuk memaksimalkan revenue dengan cara melakukan beberapa strategi marketing (misalnya, promosi atau diskon) kepada pelanggan, sehingga dengan model ini Marketing Departement bisa memberikan promosi/diskon yang tepat kepada pelanggan yang tepat pula.

Analytic Approach
------------
Tim Data Scientist akan melakukan beberapa untuk melakukan pendekatan untuk menjawab Problem Statement di atas, antara lain:
1. Visualisasi data. Melihat bagaimana persebaran data berdasarkan visualisasi grafik yang terbentuk. Kemudian, mengambil insight dari visualisasi tersebut. Metode ini merupakan salah satu metode yang cepat dan efektif untuk memahami suatu data pada tahap awal (initial judgement). Tim Data Scientist juga akan membuat interactive dashboard menggunakan tools Tableau. .....
2. Analisa menggunakan metode statistik. Metode ini digunakan untuk mengvalidasi analisa secara terukur (measureable) menggunakan metode-metode statistik, seperti statistik deskriptif atau statistik inferensial. .....
3. Machine Learning. Untuk memperkuat metode 1 dan metode 2 diatas, jadi yang akan kami lakukan adalah menganalisa data untuk menemukan pola (pattern) suatu kesamaan/perbedaan karakteristik yang tersembunyi antar nasabah/pengguna (pengelompokkan/clustering) menggunakan algoritma machine learning. Kemudian kami akan membangun model unsupervised machine learning (clustering) yang dapat membantu perusahaan untuk menemukan karakteristik-karateristik tersebut. Ketika ada nasabah baru, model ini nantinya akan berguna untuk memprediksi nasabah masuk ke dalam cluster yang mana, sehingga Marketing Departement bisa menentukan campaign marketing yang tepat.

Metric Evaluation
------------
Metrik evaluasi adalah ukuran kuantitatif yang digunakan untuk menilai kinerja dan efektivitas model machine learning. Metrik ini memberikan penjelasan tentang seberapa baik kinerja model dan dapat membantu dalam membandingkan berbagai model (benchmarking model). Pada data set ini juga tidak terdapat ground truth label, sehingga untuk pemilihan metrik evaluasi juga harus menggunakan metrik-metrik yang tidak menggunakan ground truth label.

Perlu diketahui bahwa basis metrik evaluasi pada clustering umumnya adalah menggunakan jarak (distance) antar intra-cluster (self-cluster) dan inter-cluster (neighboring-cluster), di mana dikatakan bahwa clustering yang bagus harus memiliki jarak intra-cluster yang dekat dan jarak inter-cluster yang jauh. Oleh karena itu, untuk evaluasi model unsupervised machine learning akan menggunakan metrik evaluasi silhouette score, Davies Bouldin Index (DBI), dan Calinski-Harabasz Index (CH).
- Silhouette score: mengukur jarak rata-rata antar satu sampel dengan sampel yang lainnya yang berada dalam satu cluster dan jarak rata-rata antar satu sampel dengan sampel yang lainnya yang berada pada cluster terdekat (next nearest cluster). Nilainya rentang antara -1 sampai 1, semakin mendekati 1, maka pengelompokkannya (clustering) semakin baik, atau dengan kata lain cluster satu dengan cluster yang lainnya terpisah secara baik (well separated).
- Davies Bouldin Index (DBI): konsepnya hampir sama dengan silhoutte score, yaitu menghitung jarak sampel, tetapi dalam hal ini, DBI memiliki konsep SSW (sum of square within cluster) dan SSB (sum of square between cluster). DBI mengukur jarak antar sampel dengan centroid cluster sampel tersebut dan mengukur jarak centroid antar clusternya. Score DBI yang mendekati 0 (nol), maka cluster-clusternya terpisah secara baik (well-separated).
- Calinski-Harabasz Index (CH): CH mengukur ratio dispersi antar cluster (SSB) dan intra-cluster (SSW). Tidak ada batasan nilai dama CH index, semakin besar nilainya, makanya pengelompokkanya (clustering) semakin bagus (well-separated).

Data Understanding
------------
| Columns                                            | Definition                                                   | 
| ------------------------------------------------- | ------------------------------------------------------------ |
| `CUST_ID` | Identification of Credit Card holder (Categorical) |
| `BALANCE` | Balance amount left in their account to make purchases |
| `BALANCE_FREQUENCY` | How frequently the Balance is updated, score between 0 and 1 (1 = frequently updated, 0 = not frequently updated) |
| `PURCHASES` | Amount of purchases made from account |
| `ONEOFF_PURCHASES` | Maximum purchase amount done in one-go |
| `INSTALLMENTS_PURCHASES` | Amount of purchase done in installment |
| `CASH_ADVANCE` |  Cash in advance given by the user |
| `PURCHASES_FREQUENCY` | How frequently the Purchases are being made, score between 0 and 1 (1 = frequently purchased, 0 = not frequently purchased) |
| `ONEOFF_PURCHASES_FREQUENCY` | How frequently Purchases are happening in one-go (1 = frequently purchased, 0 = not frequently purchased) |
| `PURCHASES_INSTALLMENTS_FREQUENCY` | How frequently purchases in installments are being done (1 = frequently done, 0 = not frequently done) |
| `CASH_ADVANCE_FREQUENCY` | How frequently the cash in advance being paid |
| `CASH_ADVANCE_TRX` | Number of Transactions made with "Cash in Advanced" |
| `PURCHASES_TRX` | Number of purchase transactions made |
| `CREDIT_LIMIT` | Limit of Credit Card for user |
| `PAYMENTS` | Amount of Payment done by user |
| `MINIMUM_PAYMENTS` | Minimum amount of payments made by user |
| `PRC_FULL_PAYMENT` | Percent of full payment paid by user |
| `TENURE` | Tenure of credit card service for user |

Cluster Analysis
------------
![alt text](https://github.com/PurwadhikaDev/BetaGroup_JC_DS_FT_Jogja_01_FinalProject/blob/master/reports/visualisasi2D.png)
![alt text](https://github.com/PurwadhikaDev/BetaGroup_JC_DS_FT_Jogja_01_FinalProject/blob/master/reports/visualisasi3D.png)

1. Rata-rata nilai berdasarkan fitur-fiturnya
- Terdapat 3 cluster hasil dari model KMeans-Tuned
- Mayoritas nasabah pada semua cluster lebih memilih tenure 12 bulan. Tenure yang lama juga memudahkan para nasabah dalam mengatur keuangan mereka, sehingga tidak terlalu membebani keuangan mereka.
- Cluster 0 : 2705 nasabah
    - Cluster 0 merupakan cluster dengan kelompok menengah dibandingkan dengan cluster 1 dan cluster 2. Nasabah pada cluster ini lebih seimbang dan aktif dalam menggunakan kartu kredit mereka, baik dalam hal melakukan pembelian maupun penarikan uang tunai. Mereka lebih sering melakukan pembelian dengan cicilan (installments) daripada langsung lunas (oneoff). Jadi, nasabah pada cluster ini adalah nasabah yang lebih bijak dalam menggunakan kartu kredit mereka.
- Cluster 1 : 4377 nasabah
    - Cluster 1 merupakan cluster dengan jumlah nasabah terbanyak dibanding dengan cluster lainnya. Nasabah pada cluster ini melakukan jumlah pembelian paling sedikit dengan rata-rata pembelian sebesar 199 dan rata-rata jumlah transaksi hanya 1-2 kali. Namun, mereka lebih banyak menggunakan kartu kredit mereka untuk melakukan penarikan uang tunai dengan rata-rata penarikan uang sebesar 1365 dan rata-rata sebanyak 4 kali transaksi. Kemudian, presentase pembayaran penuh (prc_full_payments) mereka juga yang paling kecil, yaitu hanya sekitar 8%. 
- Cluster 2 : 1868 nasabah
    - Cluster 0 merupakan cluster dengan total jumlah nasabah yang paling sedikit. Nasabah pada cluster ini lebih konsumtif dalam menggunakan kartu kredit mereka. Hal ini ditunjukkan dari jumlah pembelian (purchases) mereka yang paling besar, yaitu 2921 dengan rata-rata jumlah transaksi pembelian sebanyak 47 kali transaksi. Mereka juga lebih banyak melakukan pembelian dengan sistem cicilan (installments) dibandingkan dengan sistem langsung lunas (oneoff). Mereka juga memiliki rata-rata credit limit yang paling besar. Mereka juga terkadang melakukan penarikan uang tunai, tapi tidak sebanyak nasabah pada cluster 1. Kemudian, mereka memiliki presentase pembayaran penuh paling besar, yaitu 23%.

2. Purchases Type
![alt text](https://github.com/PurwadhikaDev/BetaGroup_JC_DS_FT_Jogja_01_FinalProject/blob/master/reports/purchases_type_cluster.png)
Nasabah yang termasuk ke dalam cluster 0—cluster dengan nasabah yang tergolong aktif dan seimbang dalam menggunakan kartu kredit—, lebih banyak menggunakan kartu kredit dengan sistem cicilan (installments). Kemudian pada cluster 2, cluster yang tergolong konsumtif atau sering menggunakan pembelian (purchases) lebih banyak menggunakan dengan sistem cicilan(installments) maupun lunas (oneoff). Sedangkan pada cluster 1, nasabah lebih banyak tidak menggunakan kartu kredit untuk melakukan pembelian, tapi digunakan untuk penarikan uang.

3. Remaining Limit
![alt text](https://github.com/PurwadhikaDev/BetaGroup_JC_DS_FT_Jogja_01_FinalProject/blob/master/reports/sisa_limit_cluster.png)
Pada semua cluster, mayoritas nasabah menggunakan kartu kredit mereka tidak melebihi limit yang diberikan oleh Bank. Walaupun cluster 0 tergolong cluster yang aktif dan seimbang, tetapi jika dibandingkan dengan cluster lainnya, cluster 0 memiliki presentase yang paling besar dalam hal menggunakan kartu kredit melebihi limit, yaitu sebesar 4.18%.

4. Tagihan
![alt text](https://github.com/PurwadhikaDev/BetaGroup_JC_DS_FT_Jogja_01_FinalProject/blob/master/reports/tagihan_cluster.png)
Walaupun cluster 0 tergolong cluster yang konsumtif karena sering menggunakan kartu kredit mereka untuk melakukan pembelian dengan sistem cicilan (installments) dibandingkan sistem lunas (oneoff), tapi 83% sudah tidak memiliki tagihan yang harus dibayarkan. Cluster dengan nasabah yang memiliki tagihan yang masih harus dibayarkan ada pada cluster 1, dimana cluster ini merupakan cluster yang sering melakukan penarikan uang tunai melalui kartu kredit mereka.

Kesimpulan
------------
Berdasarkan hasil analisa Tim Data Scientist Bank Beta yang telah dilakukan, maka dapat kesimpulan bahwa:
1. Setelah melakukan beberapa kali experiment, hasil metrik evaluasi, dan visualisasi cluster yang terbentuk, maka model terbaik untuk dataset yang disediakan adalah KMeans dengan parameter jumlah cluster 3 dan jumlah maksimal iterasi 300
2. Hasil cluster yang terbentuk dari model di atas sebanyak 3 cluster dengan rincian:
    - Cluster 0 sebanyak 2705 nasabah. Nasabah pada cluster ini lebih seimbang dan aktif dalam menggunakan kartu kredit mereka, baik dalam hal melakukan pembelian maupun penarikan uang tunai. Jadi, nasabah pada cluster ini adalah nasabah yang lebih bijak dalam menggunakan kartu kredit mereka.
    - Cluster 1 sebanyak 4377 nasabah. Cluster 1 merupakan cluster dengan jumlah nasabah terbanyak dibanding dengan cluster lainnya. Nasabah pada cluster ini melakukan jumlah pembelian paling sedikit dengan rata-rata pembelian sebesar $199 dan rata-rata jumlah transaksi hanya 1-2 kali. Namun, mereka lebih banyak menggunakan kartu kredit mereka untuk melakukan penarikan uang tunai.
    - Cluster 2 sebanyak 1868 nasabah. Cluster 2 merupakan cluster dengan total jumlah nasabah yang paling sedikit. Nasabah pada cluster ini lebih konsumtif dalam menggunakan kartu kredit mereka. Hal ini ditunjukkan dari jumlah pembelian (purchases) mereka yang paling besar, yaitu $2921 dengan rata-rata jumlah transaksi pembelian sebanyak 47 kali transaksi.

Rekomendasi
------------
1. Rekomendasi Strategi Marketing
Berdasarkan hasil _clustering_ yang sudah dilakukan, maka strategi marketing yang dapat dilakukan pada masing-masing cluster adalah sebagai berikut:
    - Cluster 0 :

    Karena cluster 0 adalah cluster yang paling banyak terdapat nasabah yang sering menggunakan kartu kredit lebih dari limit yang digunakan, bisa ditawarkan untuk promosi terkait penambahan limit kartu kredit kepada nasabah terutama nasabah yang tidak pempunyai tagihan. Kemudian, cluster ini terdiri dari nasabah dengan rata-rata sisa saldo untuk melakukan pembelian yang lebih rendah dibandingkan dengan cluster lainnya, sehingga mereka cenderung memiliki saldo yang lebih rendah untuk melakukan pembelian. Untuk menarik dan mempertahankan pelanggan dalam cluster ini, strategi marketing yang dapat dilakukan penawaran diskon atau penawaran khusus untuk memanfaatkan saldo yang tersisa dalam akun mereka. Selanjutnya, promosi pada produk tertentu, fokuskan pada promosi produk atau layanan yang sesuai dengan sisa saldo rendah nasabah dalam cluster ini.
    - Cluster 1 :

    Mengadakan campign atau promosi dengan tujuan agar nasabah mau bertransaksi dengan kartu kredit, terutama nasabah yang sama sekali belum pernah bertransaksi. Bisa dengan menawarkan cicilan bunga 0%. Selain itu Bank Beta disarankan untuk meningkatkan kemudahan membayar tagihan kartu kredit serta memberi edukasi kepada nasabah terutama nasabah yang masih takut menggunakan kartu kredit dikarenakan takut melebihi limitnya. Jika dilihat dari _cash advance_, Bank Beta juga bisa melakukan penawaran khusus atau insentif untuk cash advance, seperti tingkat bunga yang kompetitif atau biaya transaksi yang lebih rendah. Edukasi finansial, menyediakan informasi kepada nasabah dalam cluster ini tentang bagaimana melakukan _cash advance_ dengan bijak dan mengelola keuangan mereka, sehingga mereka tetap melakukan cash advance, namun juga membayar pembayarannya (payments). Bank Beta juga dapat, memberikan pilihan untuk mengatur batas _cash advance_ harian, mingguan, atau bulanan untuk membantu pelanggan dalam cluster ini menghindari penarikan yang berlebihan.
    - Cluster 2 :

    Cluster 2 sebagai gambaran nasabah sudah terbiasa menggunakan kartu kredit baik yang dibayar langsung maupun dijadikan cicilan dengan tenure tertentu. Untuk cluster ini bisa ditawarkan promo kenaikan limit kartu kredit serta bank diharapkan memberikan promosi terkait kesetiaan nasabah bank yang sudah lama menggunakan kartu kredit, sehingga nasabah akan terus menggunakan kartu kredit bank beta untuk bertransaksi. Selain itu, bisa juga dilakukan layanan premium, yaitu dengan menawarkan layanan premium atau produk eksklusif kepada pelanggan dalam cluster ini.
2. Rekomendasi Model
- Ketika melakukan training, mencoba dengan algoritma _unsupervised machine learning_ lainnya seperti, Gaussian Mixture, Affinity Propagation, Deep Clustering Network (DCN), Deep Adaptive Clustering (DAC), Deep Embedded Clustering (DEC), Information Maximizing Self-Augmented Training (IMSAT), dan lain sebagainya, sehingga cluster yang terbentuk mungkin lebih baik.
- Mencoba _experiment_ selain _experiment_ yang telah dilakukan, seperti training model pada fitur-fitur yang sudah dilakukan PCA, binning, dan lain sebagainya.

Dashboard
------------
https://public.tableau.com/app/profile/fajar.dwi.kurnianto/viz/CLUSTERINGCREDITCARDCUSTOMER/Dashboard1