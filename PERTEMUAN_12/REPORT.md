# PERTEMUAN 12

Management Service

## Persiapan

![0](img/0.png)

## Praktikum 12.1

1. Melihat semua layanan yang sedang berjalan

![1.1](img/1.1.png)

Banyak layanan yang aktif : 13 layanan

2. Melihat semua unit service yang ada (aktif maupun tidak)

![1.2](img/1.2.png)

3. Menganalisis waktu boot dan menemukan layanan paling lambat

![1.3](img/1.3.png)

## Tantangan

### Soal

Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu Layanannya dengan systemctl cat nama-layanan.

Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat Layanannya.

### Jawaban

Mengidentifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan `systemd-analyze blame`

![T1.1](img/T1.1.png)

1. Layanan `snapd.seeded.service`

![T1.2](img/T1.2.png)

> Nama : `snapd.seeded.service`
>
> Waktu inisialisasi : 636 ms
>
> Fungsi : Melakukan "seeding" (menanamkan atau menginisialisasi) paket-paket Snap bawaan sistem saat sistem operasi pertama kali dipasang (install) atau saat proses booting awal.

2. Layanan `dev-sdd.device`

![T1.3.1](img/T1.3.1.png)

Tidak berhasil karena `dev-sdd.device` tipe device.

![T1.3.2](img/T1.3.2.png)

> Nama : `dev-sdd.device`
>
> Waku inisialisasi : 596ms
>
> Fungsi : Memastikan sistem operasi mengenali drive tersebut saat dicolokkan atau saat komputer menyala, sehingga partisi di dalamnya bisa dibaca dan digunakan untuk menyimpan data.

Berhasil dengan perintah lain.

3. Layanan `snapd.service`

![T1.4](img/T1.4.png)

> Nama : `snapd.service`
>
> Waku inisialisasi : 491ms
>
> Fungsi : Mengunduh dan memasang aplikasi Snap baru, menjalankannya dengan aman, dan memeriksa serta mengunduh pembaruan aplikasi Snap secara otomatis di latar belakang.

## Praktikum 12.2

1. Memeriksa status ssh secara menyeluruh

![2.1](img/2.1.png)

2. Melakukan restart dan memantau perubahannya

![2.2](img/2.2.png)

3. Melihat dependensi ssh

![2.3](img/2.3.png)

4. Mengecek semua unit yang gagal di sistem

![2.4](img/2.4.png)

## Tantangan

### Soal

Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.

### Jawaban

1. Membuat file daftar-layanan.txt sekaligus mengisikan daftar nama layanan per baris

![T2.1](img/T2.1.png)

![T2.2](img/T2.2.png)

2. Membuat file cek-layanan.sh sekaligus mengisikan skripnya

![T2.3](img/T2.3.png)

![T2.4](img/T2.4.png)

3. Memberi izin eksekusi dan mengeksekusinya

![T2.5](img/T2.5.png)

4. Mengecek file laporan-layanan.log

![T.2](img/T2.6.png)

## Praktikum 12.3

1. Menyiapkan konten yang akan dilayani

![3.1.1](img/3.1.1.png)

![3.1.2](img/3.1.2.png)

2. Membuat skrip wrapper untuk server HTTP

![3.2.1](img/3.2.1.png)

![3.2.2](img/3.2.2.png)

3. Membuat berkas unit systemd untuk layanan ini

![3.3.1](img/3.1.1.png)

![3.3.2](img/3.3.2.png)

4. Menjalankan layanan dan verifikasi

![3.4](img/3.4.png)

5. Menguji fitur otomatis

![3.5](img/3.5.png)

6. Membersihkan layanan uji setelah selesai

![3.6](img/3.6.png)

## Tantangan

### Soal

Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi sebelumnya.

### Jawaban

1. Masuk ke `demo-web.service` dan mengedit skrip

![T3.1.1](img/T3.1.1.png)

![T3.1.2](img/T3.1.2.png)

2. Menyalin ke lokasi unit systemd dan meminta systemd membaca ulang berkas unit yang baru diperbarui

![T3.2](img/T3.2.png)

3. Mengaktifkan layanan dengan enable dan start

![T3.3](img/T3.3.png)

4. Menguji fitur restart otomatis

![T3.4](img/T3.4.png)

> Perbedaan :
>
> Sebelum dimodifikasi: Aplikasi langsung menyala kembali seketika (instant restart) saat crash, dan port yang digunakan masih versi default.
>
> Setelah dimodifikasi: Aplikasi menahan diri (pingsan dulu) selama 10 detik sebelum otomatis menyala kembali dengan nomor PID baru, serta sukses berjalan di port kustom 9091.

5. Membersihkan layanan uji setelah selesai

![T3.5](img/T3.5.png)

## Praktikum 12.4

1. Melihat log SSH dari satu jam terakhir

![4.1](img/4.1.png)

2. Memfilter log berprioritas error ke atas

![4.2](img/4.2.png)

3. Mengikuti log secara real-time sambil memicu aktivitas

Sebelum dikenai oleh aktivitas manapun

![4.3.1](img/4.3.1.png)

Setelah melakukan login ssh ke localhost dengan `ssh localhost`

![4.3.2](img/4.3.2.png)

4. Mengekstrak log kee berkas untuk analisis

![4.4](img/4.4.png)

## Tantangan

### Soal

Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH, simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc -l, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan

### Jawaban

![T4](img/T4.png)

1. Mengekstrak log error 24 jam terakhir dan menyimpannya ke file dengan `sudo journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt`, serta menghitung jumlah barisnya dengan `wc -l error-ssh-24jam.txt`

2. Menampilkan 10 pesan error yang paling sering muncul dengan `sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10`

## Praktikum 12.5

1. Memeriksa konfigurasi SSH saat ini

![5.1](img/5.1.png)

2. Membuat backup dan mengubah port SSH

![5.2](img/5.2.png)

3. Memvalidasi konfigurasi dan me-restart layanan

![5.3](img/5.3.png)

4. Memverifikasi port baru dengan ssh

![5.4](img/5.4.png)

5. Mengembalikan port SSH ke 22 setelah praktek

![5.5](img/5.5.png)

## Tantangan

1. Membuat backup konfigurasi dan mengeditnya

![T5.1.1](img/T5.1.1.png)

![T5.1.2](img/T5.1.2.png)

2. Memvalidasi sintaks, menerapkan perubahan, dan verifikasi pengaturan `PermitRoot` dan `MaxAuth`

![T5.2](img/T5.2.png)

3. Mengecek 20 baris log terakhir untuk memastikan SSH sehat

![T5.3](img/T5.3.png)

## Latihan

### Latihan 10.1

#### Soal

<details>
    <summary>Soal</summary>
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.

1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.

2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.

3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.
</details>

#### Jawaban

1. Semua layanan yang aktif

![L1.1.1](img/L1.1.1.png)

Memilih tiga layanan dan memeriksa statusnya :

![L1.1.2](img/L1.1.2.png)

Penjelasan fungsi tiap layanan :

> `ssh.service (OpenBSD Secure Shell server)`
>
> Service ini berfungsi untuk menyediakan jalur komunikasi jarak jauh (remote access) yang terenkripsi dan aman, sehingga kamu atau admin bisa masuk ke terminal Linux dan mengendalikan server dari komputer lain di dalam jaringan.

> `rsyslog.service (System Logging Service)`
> 
> Service ini bertugas sebagai pencatat pusat (logger) yang mengumpulkan, menyaring, dan menyimpan segala aktivitas sistem, pesan error, serta log dari berbagai aplikasi (termasuk log aktivitas login SSH) ke dalam file teks di folder /var/log/.

> `polkit.service (Authorization Manager)`
>
> Service ini (singkatan dari PolicyKit) berfungsi sebagai pengatur kebijakan hak akses yang memungkinkan proses tanpa hak istimewa (unprivileged) untuk berkomunikasi dengan proses yang memiliki hak istimewa tinggi (privileged), seperti memberikan izin kepada pengguna biasa untuk mengeksekusi perintah administratif tertentu tanpa harus sepenuhnya login sebagai root.

2. Identifikasi seluruh layanan

![L.1.2.1](img/L1.2.1.png)

Menyempitkan output menjadi 5 layanan dengan waktu inisialisasi terlama :

![L.1.2.2](img/L1.2.2.png)

3. Mendokumentasi layanan yang gagal

![L1.3](img/L1.3.png)

Tidak ditemukan adanya layanan yang gagal.

### Latihan 10.2

#### Soal

<details>
    <summary>Soal</summary>

Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.

1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.

2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.

3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.

4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.

5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.
</details>

#### Jawaban

1. Membuat file bash bernama `monitor-disk.sh` dan memberikan izin eksekusi

![L2.1.1](img/L2.1.1.png)

Mengisikan skripnya

![L2.1.2](img/L2.1.2.png)

2. Membuat berkas unit untuk menjalankan skrip

![L2.2.1](img/L2.2.1.png)

Mengisi konfigurasinya

![L.2.2.2](img/L2.2.2.png)

3. Mengaktifkan dan menjalankan layanan dan memverifikasi statusnya

![L2.3.1](img/L2.3.1.png)

Memastikan log masuk ke journal

![L2.3.2](img/L2.3.2.png)

4. Men-simulasikan crash

![L2.4](img/L2.4.png)

5. Menghentikan dan mematikan layanan

![L2.5.1](img/L2.5.1.png)

Menghapus berkas unit

![L2.5.2](img/L2.5.2.png)

Menghapus skrip yang dibuat

![L2.5.3](img/L2.5.3.png)

Menyegarkan kembali `systemd`

![L2.5.4](img/L2.5.4.png)

### Latihan 10.3

#### Soal

<details>
    <summary>Soal</summary>
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.

1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.

2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd -t, reload.

3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).

4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
</details>

#### Jawaban

1. Mencari error, menghitung jumlah barisnya, dan menyimpannya ke berkas

![L3.1](img/L3.1.png)

2. Melakukan 3 perubahan keamanan pada `/etc/ssh/ssgd_config` melalui alur aman

![L3.2.1](img/L3.2.1.png)

Isi skrip

![L3.2.2](img/L3.2.2.png)

3. Memverifikasi 3 hal

![L3.3.1](img/L3.3.1.png)

![L3.3.2](img/L3.3.2.png)

4. Mengembalikan konfigurasi SSH ke kondisi semula

![L3.4](img/L3.4.png)