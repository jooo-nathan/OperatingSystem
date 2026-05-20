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

Mengidentifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan `systemd-analyze blame`

![T1.1](img/T1.1.png)

1. Fungsi `snapd.seeded.service`

![T1.2](img/T1.2.png)

2. Fungsi `dev-sdd.device`

![T1.3.1](img/T1.3.1.png)

Tidak berhasil karena `dev-sdd.device` tipe device.

![T1.3.2](img/T1.3.2.png)

Berhasil dengan perintah lain.

3. Fungsi `snapd.service`

![T1.4](img/T1.4.png)

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

## Praktikum 12.3

## Tantangan

## Praktikum 12.4

## Praktikum 12.5

## Tantangan

## Latihan

### Latihan 10.1

### Latihan 10.2

### Latihan 10.3