**# LAPORAN UTS KEAMANAN JARINGAN**



**\*\*Nama:\*\*** Nadia Salma Nurhidayah  

**\*\*NIM:\*\*** 24552011044  

**\*\*Kasus:\*\*** 8



**---**



**## IDENTIFIKASI KASUS**



Jumlah digit NIM:



2 + 4 + 5 + 5 + 2 + 0 + 1 + 1 + 0 + 4 + 4 = 28



Hasil modulo 10:



28 mod 10 = 8



Dengan demikian, kasus yang dikerjakan adalah Kasus 8.



**---**



**# TUGAS 1 — DOCKER DAN VOLUME**



**## 1. Tujuan**



Membuktikan bahwa data pada Docker Volume tetap tersimpan meskipun container awal dihapus serta menguji komunikasi antara container attacker dan target menggunakan Docker Compose.



**## 2. Langkah Praktikum**



1\. Membuat Docker Volume dengan nama \`vol-k8\`.

2\. Membuat container sementara bernama \`w-k8\`.

3\. Menyimpan NIM ke dalam file \`laporan-k8.txt\` pada volume.

4\. Menghapus container sementara \`w-k8\`.

5\. Membaca kembali file dari container baru menggunakan volume yang sama.

6\. Menjalankan dua service menggunakan Docker Compose, yaitu attacker dan target.

7\. Menguji akses halaman Nginx dari container attacker.



**## 3. Hasil Pengujian Docker Volume**



Setelah container awal dihapus, file berhasil dibaca kembali menggunakan container baru.



NIM yang berhasil ditampilkan:



**\*\*24552011044\*\***



Hal ini menunjukkan bahwa data tetap tersimpan pada Docker Volume meskipun container awal sudah dihapus.



**## 4. Hasil Pengujian Nginx**



Docker Compose berhasil menjalankan dua container, yaitu:



\- \`k8-attacker-1\` dengan image Alpine.

\- \`k8-target-1\` dengan image Nginx.



Pengujian dilakukan dari container attacker menuju target menggunakan perintah \`wget\`. Halaman Nginx berhasil diakses dan menampilkan respons HTML.



**## 5. Bukti Praktikum**



**### Bukti 1 — Docker Volume**



![Bukti Docker Volume](bukti%20screenshot/tugas1-volume.jpg.png)



**### Bukti 2 — Halaman Nginx**



![Bukti Nginx](bukti%20screenshot/tugas1-nginx.jpg.png)



**## 6. Kesimpulan**



Docker Volume memungkinkan data tetap tersimpan secara terpisah dari siklus hidup container. Dengan demikian, file tetap dapat dibaca oleh container baru selama menggunakan volume yang sama.



Selain itu, Docker Compose berhasil menjalankan container attacker dan target dalam jaringan internal sehingga attacker dapat mengakses layanan Nginx pada target.



**---**



**# TUGAS 2 — KRIPTOGRAFI**



**## 1. Tujuan**



Menerapkan enkripsi AES-256 untuk melindungi isi laporan, melakukan dekripsi untuk mengembalikan data asli, serta membandingkan nilai hash SHA-256. Selain itu, membuat sertifikat digital self-signed menggunakan OpenSSL.



**## 2. Langkah Praktikum**



1\. Menyiapkan image Docker yang berisi OpenSSL.

2\. Membuat file laporan dengan identitas NIM.

3\. Mengenkripsi file menggunakan AES-256-CBC dengan metode PBKDF2.

4\. Menghitung hash SHA-256 dari file asli.

5\. Melakukan dekripsi terhadap file terenkripsi.

6\. Menghitung hash SHA-256 dari hasil dekripsi.

7\. Membuat sertifikat digital self-signed dengan Common Name \`k8.uts.local\`.

8\. Menampilkan informasi Subject, Issuer, dan masa berlaku sertifikat.



**## 3. Hasil Pengujian AES-256 dan SHA-256**



File laporan berhasil dienkripsi menggunakan algoritma AES-256-CBC dengan kata sandi \`kunci-k8-2026\`.



Setelah proses dekripsi, isi file berhasil dikembalikan seperti semula.



Nilai hash SHA-256 file asli dan hasil dekripsi dibandingkan. Kedua nilai hash harus sama untuk membuktikan bahwa isi file hasil dekripsi identik dengan file asli.

Nilai hash SHA-256 yang diperoleh dari pengujian:

- File asli: `5dca5a64547acfa3ad235fc4fa9eecc8ba8feae8d7f94033aed9a5d5278cdb9e`
- Hasil dekripsi: `5dca5a64547acfa3ad235fc4fa9eecc8ba8feae8d7f94033aed9a5d5278cdb9e`

Kedua nilai hash sama, sehingga isi file hasil dekripsi identik dengan file asli.



**## 4. Hasil Pembuatan Sertifikat**

\- Tanggal mulai berlaku: 24 November 2026.

\- Tanggal berakhir: 24 Desember 2026.



Sertifikat digital berhasil dibuat menggunakan OpenSSL dengan jenis self-signed certificate.



Informasi sertifikat:



\- Common Name: \`k8.uts.local\`

\- Subject: \`CN=k8.uts.local\`

\- Issuer: \`CN=k8.uts.local\`

\- Masa berlaku: 30 hari.



**## 5. Perbedaan Sertifikat Self-Signed dan Sertifikat CA**



Sertifikat self-signed ditandatangani oleh pemilik sertifikat itu sendiri sehingga tidak memperoleh pengesahan dari Certificate Authority (CA) tepercaya. Sementara itu, sertifikat CA ditandatangani oleh Certificate Authority yang berfungsi memverifikasi identitas pemilik sertifikat sehingga lebih mudah dipercaya oleh sistem dan browser.



**## 6. Bukti Praktikum**



**### Bukti 1 — Perbandingan Hash SHA-256**



![Bukti Hash SHA-256](bukti%20screenshot/tugas2-hash.png)



**### Bukti 2 — Sertifikat Self-Signed**



![Bukti Sertifikat](bukti%20screenshot/tugas2-sertifikat.png)





**## 7. Kesimpulan**



Praktikum ini menunjukkan bahwa OpenSSL dapat digunakan untuk mengenkripsi dan mendekripsi file menggunakan AES-256. Kesamaan nilai hash SHA-256 menunjukkan bahwa data hasil dekripsi sama dengan data asli. Selain itu, sertifikat self-signed berhasil dibuat untuk memahami penggunaan sertifikat digital dalam keamanan komunikasi.



**---**



**## Tugas 3 — ARP Spoofing dan Mitigasi**



**### 1. Tujuan**

Mengamati tabel ARP pada jaringan Docker serta memahami pentingnya penggunaan static ARP sebagai salah satu langkah mitigasi terhadap manipulasi ARP.



**### 2. Persiapan Lingkungan**

Lingkungan pengujian menggunakan Docker dengan jaringan \`lab-arp_lab_network\`. Image dan lingkungan lab telah dipersiapkan untuk melakukan pengamatan jaringan.



**\*\*Bukti persiapan:\*\***



![Persiapan lingkungan lab]\(bukti%20screenshot/tugas3-persiapan.png)



**### 3. Hasil Pengamatan ARP Awal**

Pengamatan dilakukan menggunakan perintah \`ip neigh show\`. Hasilnya menampilkan gateway dengan alamat IP \`192.168.240.1\` dan MAC address \`aa:ad:a1:a5:05:af\`.



Status entri yang muncul adalah \`REACHABLE\`, yang menunjukkan bahwa alamat tetangga jaringan berhasil terdeteksi.



**\*\*Bukti ARP awal:\*\***



![Hasil pengamatan ARP awal]\(bukti%20screenshot/tugas3-arp-awal.png)



**### 4. Pengujian Mitigasi Static ARP**

Pengujian konfigurasi static ARP dicoba pada container pengamatan. Namun, proses tersebut tidak berhasil karena container tidak memiliki izin administrasi jaringan.



Pesan yang muncul adalah \`RTNETLINK answers: Operation not permitted\`.



Dengan demikian, konfigurasi static ARP belum berhasil diterapkan dan belum dapat diverifikasi pada pengujian ini.



**\*\*Bukti kendala pengujian:\*\***



![Hasil percobaan mitigasi static ARP]\(bukti%20screenshot/tugas3-arp-mitigasi.png)



**### 5. Kesimpulan**

Berdasarkan pengujian, tabel ARP awal berhasil diamati dan menampilkan alamat gateway beserta MAC address-nya. Pengujian konfigurasi static ARP belum berhasil karena keterbatasan izin pada container. Dari kegiatan ini dapat dipahami bahwa pengamatan tabel ARP membantu mengenali perangkat dalam jaringan, sedangkan static ARP merupakan salah satu pendekatan untuk membantu melindungi pemetaan alamat IP dan MAC. Mitigasi lain selain static ARP adalah Dynamic ARP Inspection (DAI). 
DAI membantu memeriksa validitas pasangan alamat IP dan MAC sehingga 
paket ARP yang tidak sesuai dapat diblokir.



**## Tugas 4 — Analisis Handshake WPA2**



**### 1. Tujuan**

Memahami proses autentikasi WPA2 melalui four-way handshake serta mengenali fungsi setiap pesan dalam proses pembentukan kunci keamanan antara client dan Access Point.



**### 2. Persiapan File**

File pengujian yang disediakan terdapat pada folder \`01-sumber-lab/samples\`, yaitu:

\- \`handshake-k8.cap\`

\- \`wordlist-k8.txt\`



**\*\*Bukti lokasi file:\*\***



![Lokasi file handshake dan wordlist]\(bukti%20screenshot/tugas4-file-handshake.png)



**### 3. Analisis Four-Way Handshake**



Proses WPA2 menggunakan empat pesan untuk membentuk dan memasang kunci keamanan:



1\. **\*\*Message 1:\*\*** Access Point mengirim ANonce kepada client.

2\. **\*\*Message 2:\*\*** Client menghasilkan SNonce dan mengirimkannya bersama MIC sebagai bukti autentikasi.

3\. **\*\*Message 3:\*\*** Access Point mengirim informasi pemasangan kunci beserta MIC kepada client.

4\. **\*\*Message 4:\*\*** Client mengirim konfirmasi bahwa proses pemasangan kunci telah diterima.



Setelah keempat pesan selesai, client dan Access Point dapat berkomunikasi menggunakan kunci yang telah dibentuk.



**### 4. Hasil Pengujian**

File capture dan wordlist berhasil ditemukan pada folder sampel. Namun, pengujian pencarian kata sandi belum dijalankan sehingga status \`KEY FOUND\` atau \`KEY NOT FOUND\` belum dapat ditentukan.



**### 5. Kesimpulan**

Four-way handshake WPA2 merupakan proses autentikasi dan pembentukan kunci keamanan antara client dan Access Point. Keempat pesan memiliki fungsi yang saling berkaitan untuk memastikan kedua perangkat memiliki informasi kunci yang sesuai.



**## Tugas 5 — ICMP dengan Scapy**



**### 1. Tujuan**

Memahami penggunaan protokol ICMP, nilai TTL, serta tipe pesan ICMP melalui pengamatan jaringan.



**### 2. Persiapan**

Script \`kirim_icmp.py\` ditemukan di folder \`01-sumber-lab/kasus/k5-scapy\`. File pendukung \`handshake-k5.cap\` dan \`wordlist-k5.txt\` juga ditemukan di folder \`01-sumber-lab/samples\`.



**\*\*Bukti persiapan:\*\***



![Persiapan Tugas 5]\(bukti%20screenshot/tugas5-persiapan.png)



**### 3. Konsep ICMP**

\- **\*\*TTL (Time To Live):\*\*** menentukan batas hop paket IP sebelum dibuang.

\- **\*\*ICMP Echo Reply:\*\*** pesan balasan dari perangkat terhadap Echo Request.

\- **\*\*Smurf Attack:\*\*** serangan DoS yang memanfaatkan ICMP dan broadcast untuk memperbesar lalu lintas menuju target.



**### 4. Mitigasi**

Mitigasi Smurf Attack dapat dilakukan dengan menonaktifkan IP-directed broadcast, menyaring lalu lintas ICMP yang tidak diperlukan, dan memantau lonjakan trafik jaringan.



**### 5. Hasil Pengamatan**

Script pengujian ditemukan, tetapi pengiriman paket belum dijalankan. Oleh karena itu, nilai TTL dan tipe ICMP balasan belum diperoleh.



**### 6. Kesimpulan**

ICMP berguna untuk komunikasi diagnostik jaringan. TTL membantu membatasi perjalanan paket, sedangkan pengaturan broadcast dan penyaringan trafik membantu mengurangi risiko penyalahgunaan ICMP.



**## Tugas 6 — SYN Flood dan Three-Way Handshake**



**### 1. Tujuan**

Memahami proses pembentukan koneksi TCP melalui three-way handshake serta mengetahui dampak SYN flood terhadap ketersediaan layanan server.



**### 2. Persiapan Lingkungan**

Folder konfigurasi Docker Compose ditemukan pada:



\`01-sumber-lab/b/b3-syn-flood/docker-compose.yml\`



File tersebut digunakan sebagai konfigurasi lingkungan lab Tugas 6.



**\*\*Bukti persiapan:\*\***



![Persiapan lab Tugas 6]\(bukti%20screenshot/tugas6-persiapan.png)



**### 3. Three-Way Handshake**

Proses pembentukan koneksi TCP terdiri dari tiga tahap:



1\. **\*\*SYN:\*\*** Client mengirim permintaan untuk memulai koneksi kepada server.

2\. **\*\*SYN-ACK:\*\*** Server membalas permintaan dan menyatakan kesiapan menerima koneksi.

3\. **\*\*ACK:\*\*** Client mengirim konfirmasi sehingga koneksi TCP terbentuk.



**### 4. Pengertian SYN Flood**

SYN flood merupakan serangan Denial of Service (DoS) yang memanfaatkan banyaknya permintaan koneksi SYN sehingga sumber daya server dapat terkuras.



**### 5. Mitigasi**

Beberapa langkah mitigasi yang dapat diterapkan:

\- Menggunakan SYN cookies.

\- Menerapkan pembatasan laju koneksi.

\- Menggunakan firewall untuk menyaring trafik.

\- Memantau koneksi setengah terbuka melalui status SYN_RECV.



**### 6. Hasil Pengujian**

File konfigurasi Docker Compose berhasil ditemukan. Simulasi SYN flood dan pengamatan paket selama serangan tidak dijalankan. Oleh karena itu, jumlah SYN_RECV sebelum dan saat serangan serta bukti paket SYN, SYN-ACK, dan ACK belum diperoleh.



Docker Compose mendefinisikan layanan target menggunakan Nginx dan layanan attacker menggunakan image uts-kali-tools. Kedua layanan berada pada jaringan internal bernama lab. Pengujian SYN flood tidak dijalankan, sehingga jumlah koneksi SYN_RECV sebelum dan selama serangan tidak tersedia.

**### 7. Kesimpulan**

Three-way handshake merupakan mekanisme penting dalam pembentukan koneksi TCP. SYN flood dapat mengganggu ketersediaan layanan dengan membebani sumber daya server. Pemantauan koneksi dan penerapan mekanisme mitigasi dapat membantu mengurangi risikonya.



**## Tugas 7 — DNS Exfiltration**



**### 1. Tujuan**

Memahami konsep DNS exfiltration serta cara mendeteksi pola komunikasi DNS yang mencurigakan melalui analisis log.



**### 2. Persiapan Lingkungan**

File konfigurasi Docker Compose ditemukan pada folder \`01-sumber-lab/b/b4-dns-exfil/docker-compose.yml\`.



Script analisis DNS juga ditemukan pada folder \`01-sumber-lab/kasus/k9-dns-detect/analisis_dns.py\`.



**\*\*Bukti persiapan:\*\***



![Persiapan Tugas 7]\(bukti%20screenshot/tugas7-persiapan.png)



**### 3. Konsep DNS Exfiltration**

DNS exfiltration merupakan teknik penyalahgunaan protokol DNS untuk mengirimkan data keluar melalui permintaan DNS. Data dapat dikodekan ke dalam subdomain sehingga aktivitasnya dapat terlihat pada log DNS.



**### 4. Analisis dan Deteksi**

Analisis DNS dapat dilakukan dengan memperhatikan:

\- Subdomain yang panjang atau tidak biasa.

\- Banyaknya permintaan DNS ke domain tertentu.

\- Pola label domain yang tampak seperti data terenkode.

\- Frekuensi permintaan DNS yang tidak wajar.

DNS exfiltration sulit diblokir oleh firewall biasa karena komunikasi DNS 
sering diizinkan untuk kebutuhan akses internet. Salah satu indikator 
deteksinya adalah subdomain yang panjang dan memiliki pola karakter 
tidak biasa atau menyerupai data terenkode.


Script \`analisis_dns.py\` disediakan untuk membantu proses analisis log DNS.



**### 5. Hasil Pengujian**

Folder konfigurasi dan script analisis berhasil ditemukan. Pengiriman data melalui DNS dan pengujian eksfiltrasi belum dijalankan. Oleh karena itu, hasil deteksi label hex dan hasil decoding belum tersedia.



**### 6. Mitigasi**

\- Memantau dan mencatat permintaan DNS.

\- Membatasi akses DNS hanya melalui resolver yang diizinkan.

\- Mendeteksi subdomain yang panjang dan pola permintaan tidak biasa.

\- Menggunakan DNS filtering dan monitoring jaringan.



**### 7. Kesimpulan**

DNS dapat disalahgunakan sebagai jalur pengiriman data. Analisis log DNS membantu mengidentifikasi pola komunikasi mencurigakan sehingga aktivitas yang berpotensi menjadi DNS exfiltration dapat dideteksi lebih awal.