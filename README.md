# **Transjakarta**

# Latar Belakang

Transjakarta, sebagai sistem transportasi publik terbesar di DKI Jakarta, memiliki peran yang sangat krusial dalam menunjang aktivitas harian masyarakat perkotaan. Dengan cakupan jaringan yang terus berkembang, peningkatan jumlah armada, dan penambahan koridor serta rute baru, jumlah penumpang Transjakarta terus mengalami peningkatan dari tahun ke tahun. Seiring dengan hal tersebut, tantangan dalam pengelolaan operasional dan pelayanan publik pun semakin kompleks.

Salah satu aset yang sangat berharga namun seringkali belum dimanfaatkan secara optimal adalah data perjalanan penumpang yang terekam secara digital melalui sistem tap-in dan tap-out. Setiap transaksi tap kartu elektronik mencatat berbagai informasi penting seperti waktu naik dan turun, titik pemberangkatan dan tujuan (berbasis koordinat geografis), rute atau koridor yang digunakan, serta nominal pembayaran. Informasi ini menyimpan potensi besar untuk dianalisis guna mendukung pengambilan keputusan yang lebih tepat dan berbasis data.

Melalui pemanfaatan data transaksi ini, kita dapat mengidentifikasi berbagai pola perjalanan penumpang, seperti waktu-waktu sibuk, rute paling padat, segmentasi pengguna berdasarkan usia atau metode pembayaran, dan tingkat kepatuhan terhadap prosedur tap-in/tap-out. Selain itu, data ini juga dapat digunakan untuk mengevaluasi efisiensi operasional rute tertentu, meninjau efektivitas tarif, serta merancang strategi peningkatan layanan yang lebih responsif terhadap kebutuhan pengguna.

Sayangnya, seperti halnya data besar pada umumnya, tidak semua informasi tercatat dengan lengkap dan bersih. Terdapat sejumlah transaksi yang tidak memiliki catatan tap-out atau data lokasi yang tidak lengkap. Ketidaksempurnaan ini dapat menjadi tantangan dalam analisis, namun sekaligus membuka peluang untuk melakukan data cleaning, imputasi, serta eksplorasi lebih dalam terhadap perilaku pengguna.

Melalui proyek ini, dilakukan eksplorasi dan analisis mendalam terhadap data transaksi penumpang Transjakarta, dengan tujuan utama untuk menggali insight yang bermanfaat bagi peningkatan kualitas layanan, efisiensi operasional, serta pengalaman pengguna secara keseluruhan. Dengan analisis yang tepat, data perjalanan ini tidak hanya menjadi arsip digital semata, tetapi juga menjadi dasar yang kuat untuk membangun sistem transportasi publik yang lebih cerdas, inklusif, dan berkelanjutan di masa depan.

# Rumusan Masalah

Adapun rumusan masalah yang diangkar dari pengerjaan data ini adalah:
1. Apakah ada perbedaan distribusi nilai payAmount antara transaksi dengan dan tanpa tapOutTime?

2. Seberapa besar pengaruh keberadaan tapOutTime terhadap nilai payAmount?

3. Bagaimana distribusi usia pengguna layanan TransJakarta berdasarkan kelompok usia?

4. Apa yang dapat disimpulkan dari data transaksi terkait perilaku pengguna

# Data Under Standing

Langkah awal ini penting dilakukan untuk memahami struktur dan karakteristik dataset secara menyeluruh sebelum melanjutkan ke tahap analisis. Melalui proses ini, kita juga dapat mengidentifikasi potensi permasalahan atau kejanggalan dalam data, sehingga dapat dirumuskan langkah-langkah penanganan yang tepat pada tahap selanjutnya, yaitu Data Cleaning.

Berjumlahkan 22 Kolom, berikut penjelasan masing-masing kolom nya

* `transID`: Merupakan identifikasi unik untuk setiap transaksi yang terjadi dalam sistem.

* `payCardID`: Kode identitas khusus yang menunjukkan kartu elektronik yang digunakan oleh penumpang saat transaksi.

* `payCardBank`: Nama institusi perbankan yang mengeluarkan kartu pembayaran yang digunakan oleh penumpang.

* `payCardName`: Nama pemilik kartu sebagaimana tercatat dalam sistem, biasanya sesuai dengan data kepemilikan kartu.

* `payCardSex`: Informasi jenis kelamin dari pemilik kartu (misalnya: laki-laki atau perempuan).

* `payCardBirthDate`: Tahun kelahiran dari pemegang kartu, digunakan untuk mengelompokkan pengguna berdasarkan usia.

* `corridorID`: Nomor identifikasi dari koridor atau jalur Transjakarta yang digunakan dalam perjalanan.

* `corridorName`: Nama dari koridor atau rute yang dilalui, biasanya mencakup nama halte awal dan akhir.

* `direction`: Arah perjalanan dalam rute, dengan nilai 0 menandakan arah pergi dan 1 untuk arah pulang.

* `tapInStops`: Kode identifikasi halte tempat penumpang pertama kali masuk atau melakukan tap-in.

* `tapInStopsName`: Nama halte di mana penumpang memulai perjalanannya atau melakukan tap-in.

* `tapInStopsLat`: Koordinat lintang (latitude) lokasi halte tempat penumpang tap-in.

* `tapInStopsLon`: Koordinat bujur (longitude) lokasi halte tempat penumpang tap-in.

* `stopStartSeq`: Urutan halte awal dalam rute perjalanan sesuai dengan jalur koridor yang digunakan.

* `tapInTime`: Waktu dan tanggal saat penumpang melakukan tap-in di halte keberangkatan.

* `tapOutStops`: Kode halte tempat penumpang keluar atau menyelesaikan perjalanan dengan tap-out.

* `tapOutStopsName`: Nama halte tujuan atau tempat penumpang melakukan tap-out.

* `tapOutStopsLat`: Koordinat lintang dari halte tempat penumpang menyelesaikan perjalanan.

* `tapOutStopsLon`: Koordinat bujur dari halte tap-out penumpang.

* `stopEndSeq`: Posisi atau urutan halte akhir dalam rute, berdasarkan alur perjalanan koridor.

* `tapOutTime`: Waktu dan tanggal saat penumpang melakukan tap-out di halte tujuan.

* `payAmount`: Besarnya biaya yang dibayarkan penumpang untuk perjalanan tersebut; bisa bernilai nol untuk perjalanan gratis.

# Data Cleaning 
Data Cleaning atau pembersihan data adalah tahap penting dalam proses analisis data yang bertujuan untuk memastikan kualitas dan keakuratan dataset sebelum dianalisis lebih lanjut. Pada tahap ini, data diperiksa dan diperbaiki dari berbagai masalah seperti nilai yang hilang (missing values), data duplikat, inkonsistensi format, kesalahan penulisan, dan nilai-nilai yang tidak logis. Misalnya, data yang seharusnya numerik tetapi tersimpan sebagai teks, atau entri waktu yang tidak lengkap perlu diperbaiki agar tidak mempengaruhi hasil analisis.

1. Menghindari Kesalahan Analisis

Data yang tidak bersih bisa menyebabkan kesalahan dalam interpretasi. Misalnya, jika terdapat data ganda atau nilai yang tidak sesuai, maka hasil analisis statistik seperti rata-rata, median, atau korelasi bisa menyesatkan. Hal ini akan berdampak pada keputusan yang diambil dari hasil analisis tersebut.

2. Menghapus Duplikasi Data

Duplikasi bisa terjadi karena kesalahan input, sistem yang merekam dua kali, atau penggabungan beberapa sumber data. Jika tidak dihapus, nilai-nilai seperti jumlah total, persentase, dan distribusi bisa terdistorsi dan menghasilkan informasi yang tidak akurat.

3. Menangani Data yang Hilang (Missing Values)

Data yang kosong dapat menghambat proses analisis, terutama pada algoritma statistik dan machine learning yang membutuhkan data lengkap. Mengisi nilai kosong (imputasi), menghapus baris tertentu, atau menandai sebagai kategori tersendiri dapat meningkatkan kualitas data dan membuat model lebih stabil.

4. Standarisasi Format dan Struktur

Data yang tidak seragam—misalnya perbedaan penulisan tanggal, satuan ukuran, atau format teks—dapat menyulitkan proses pengolahan. Standarisasi memastikan seluruh data mudah dibaca oleh manusia dan diproses oleh sistem secara otomatis tanpa kesalahan.

5. Menghilangkan Outlier atau Nilai Tak Wajar

Outlier adalah nilai yang jauh berbeda dari mayoritas data. Dalam beberapa kasus, outlier adalah kesalahan input atau anomali sistem. Mengidentifikasi dan menangani nilai-nilai ini penting untuk menjaga agar analisis tetap mewakili kondisi umum, bukan hanya kasus-kasus ekstrem.

6. Meningkatkan Kinerja Model Analitik

Model prediktif atau statistik bekerja optimal jika datanya bersih dan konsisten. Data yang tidak bersih dapat menyebabkan model bias, akurasi rendah, atau bahkan gagal dijalankan. Oleh karena itu, pembersihan data adalah bagian penting dalam pra-pemrosesan sebelum modeling.

7. Menjamin Konsistensi Data Antar-Kolom

Dalam banyak dataset, antar-kolom sering saling berhubungan. Inkonsistensi antar-kolom—misalnya data waktu yang tidak selaras dengan urutan kejadian—dapat merusak logika analisis. Pembersihan data menjaga hubungan ini tetap logis dan selaras.

8. Meningkatkan Kredibilitas dan Kepercayaan terhadap Data

Data yang sudah dibersihkan akan lebih dipercaya oleh pengguna akhir seperti manajer, peneliti, atau analis. Dengan data yang kredibel, proses pengambilan keputusan menjadi lebih yakin dan berbasis bukti yang valid.

# Data Analysist

Setelah proses data cleaning dilakukan dan dataset berada dalam kondisi yang bersih serta konsisten, tahap selanjutnya adalah melakukan analisis data. Tahapan ini bertujuan untuk menggali informasi yang terkandung dalam data melalui eksplorasi, visualisasi, dan pengukuran statistik.

Melalui analisis ini, kita dapat mengidentifikasi pola-pola penting, hubungan antar variabel, serta anomali yang mungkin terjadi. Langkah ini menjadi krusial dalam memahami karakteristik data, mengevaluasi performa sistem, hingga menemukan insight yang dapat digunakan untuk pengambilan keputusan strategis berbasis data.

Analisis dilakukan dengan pendekatan deskriptif dan eksploratif, menggunakan berbagai teknik visualisasi serta perhitungan numerik, guna menghasilkan pemahaman yang mendalam terhadap perilaku dan karakteristik pengguna serta sistem yang dianalisis.

# Visualisasi Tableau

Data bersih yang telah disimpan sebelumnya divisualisasikan dengan Tableau. Berikut ini adalah link tableau project ini:

https://public.tableau.com/views/DashboardCapstone2_17530190832810/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
