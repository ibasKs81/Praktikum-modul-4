# Praktikum Mikrokontroler - Modul I: Percabangan dan Perulangan

**Nama:** Ibnu Abbas  
**NIM:** H1H024038  
**Mata Kuliah:** TK244005 - Praktikum Mikrokontroler  
**Program Studi:** Informatika, Universitas Jenderal Soedirman  

---

## 📌 Deskripsi Repositori
Praktikum ini bertujuan untuk mengimplementasikan konfigurasi modul Analog to Digital Converter (ADC) dan teknik Pulse Width Modulation (PWM) pada Arduino. Percobaan melibatkan penggunaan potensiometer untuk menghasilkan tegangan analog yang kemudian dikonversi menjadi data digital untuk mengendalikan motor servo dan intensitas cahaya LED.
---
## 🔬 Analisis Percobaan 1
### 1. Apa fungsi perintah analogRead() pada rangkaian ini?
Fungsi ini digunakan untuk membaca tegangan analog kontinu dari potensiometer dan menangkap amplitudo sinyal tersebut.
### 2. Mengapa diperlukan fungsi map() dalam program tersebut?
Pada kondisi nilai delay diatas 100 yang mana ketika baru menyala nilainya adalah 1000
### 3.  Apa fungsi dari perintah delay(timeDelay)? 
Fungsi map() diperlukan untuk mengonversi nilai digital hasil pembacaan ADC (0–1023) menjadi rentang nilai yang dapat dipahami oleh motor servo (dalam kasus ini dibatasi ke 30–150) sehingga terjadi sinkronisasi gerakan.
### 4. Penjelasan Program Modifikasi:
Program menggunakan fungsi map(val, 0, 1023, 30, 150) sehingga nilai ADC terendah (0) akan menghasilkan sudut 30° dan nilai tertinggi (1023) akan menghasilkan sudut 150°.
```cpp
#include <Servo.h>

Servo myservo;  
int potPin = A0;  // Input analog dari potensio [cite: 53]
int val;    

void setup() {
  myservo.attach(9); // Servo terhubung ke pin PWM
}

void loop() {
  val = analogRead(potPin);            // Membaca nilai ADC (0-1023)
  // Modifikasi: Membatasi rentang sudut ke 30-150 derajat
  val = map(val, 0, 1023, 30, 150);     
  myservo.write(val);                  
  delay(15);                           
}
```
---
## Analisa Percobaan 2
### 1. Gambarkan rangkaian schematic 5 LED running yang digunakan pada percobaan!
![LED Circuit](skematikp2)
### 2. Jelaskan bagaimana program membuat efek LED berjalan dari kiri ke kanan!
Ketika program menyalakan pin 7 maka program akan beralih ke loppingan for yang kedua dimana isinya dalah mengurangi pin output sehingga pin yang aktif adalah dari kiri ke kanan.
### 3.Jelaskan bagaimana program membuat LED kembali dari kanan ke kiri!
Porogram menjalankan looping for pertama yang mengaktifkan pin 2 hingga ke 8
### 4.Buatkan program agar LED menyala tiga LED kanan dan tiga LED kiri secara bergantian  dan berikan penjelasan disetiap baris kode nya dalam bentuk README.md!
```cpp
int timer = 100;           
// delay. Semakin tinggi angkanya, semakin lambat waktunya. 
void setup() { 
// gunakan loop for untuk menginisialisasi setiap pin sebagai 
output: 
for (int ledPin = 2; ledPin < 4; ledPin++) { 
pinMode(ledPin, OUTPUT); 
} 
} 
void loop() { 
// looping dari pin rendah ke tinggi 
for (int ledPin = 2; ledPin < 4; ledPin++) { 
// hidupkan LED pin nya: 
digitalWrite(ledPin, HIGH); 
delay(timer); 
// matikan pin LED nya: 
digitalWrite(ledPin, LOW); 
}
for (int ledPin = 3; ledPin >= 2; ledPin--) { 
// menghidupkan pin: 
digitalWrite(ledPin, HIGH); 
delay(timer); 
// mematikan pin: 
digitalWrite(ledPin, LOW); 
} 
}
```
Program tetap sama hanya saja wiringnya dijadikan 1 sehingga tetap bisa menghasilkan output yang sama berikut adalah Wiringnya
![LED Pararel](wiringp3)



## 📁 Penjelasan File Program

### 1. `Praktikum_Percobaan_1.ino` (Percabangan)
**Tujuan Kode:** File ini berisi program untuk mendemonstrasikan fungsi struktur logika percabangan menggunakan instruksi `if-else`. Program ini bertujuan untuk mengevaluasi kondisi parameter batas waktu tunda (*delay*) dan secara dinamis mengubah kecepatan fase kedipan sebuah LED tunggal tanpa memerlukan intervensi manual dari pengguna. Pada tugas modifikasi praktikum ini, program dirancang agar siklus nyala LED berubah secara bertahap: mulai dari fase berkedip cepat, kemudian memelan (kecepatan sedang), dan pada akhirnya sistem akan menahan LED dalam kondisi mati secara permanen (*reset*).

### 2. `Modul_1_Percobaann_2.ino` (Perulangan)
**Tujuan Kode:** File ini berisi program untuk mendemonstrasikan efisiensi struktur kendali perulangan menggunakan instruksi `for` *loop*. Program ini bertujuan untuk memanipulasi rentetan banyak pin digital secara otomatis hanya dengan sedikit baris kode guna menciptakan efek visual pergerakan cahaya pada susunan enam buah LED. Pada tugas modifikasi praktikum ini, instruksi perulangan direkayasa untuk membagi deretan 6 LED menjadi dua blok terpisah (3 LED di sisi kiri dan 3 LED di sisi kanan), di mana program akan memerintahkan kedua kelompok tersebut untuk menyala secara bergantian secara terus-menerus.

---

## 📸 Dokumentasi Praktikum
### 1. Dokumentasi Percobaan
Percobaan 1:
![Lampiran percobaan 1 Praktikum](WhatsApp%20Image%202026-04-07%20at%2013.12.22.jpeg)
Percobaan 2: 
![Lampiran percobaan 2 Praktikum](WhatsApp%20Image%202026-04-07%20at%2013.12.27.jpeg)

### 2. Skematik Rangkaian
Skematik Rangkaian prcobaan 1
![Skematik Rangkaian prcobaan 1](Screenshot%202026-04-08%20015201.png)
Skematik Rangkaian prcobaan 2
![Tautan Gambar Skematik_2 Di Sini](Screenshot%202026-04-08%20015551.png)

*Laporan praktikum lengkap beserta analisis data tersedia pada direktori utama repositori ini dalam format dokumen.*
