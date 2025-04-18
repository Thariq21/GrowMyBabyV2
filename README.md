# GrowMyBaby – Deteksi Dini Stunting pada Anak

**GrowMyBaby** adalah sebuah prototipe berbasis IoT yang dirancang untuk mendeteksi potensi stunting pada anak usia dini. Sistem ini menggunakan sensor untuk mengukur berat badan dan tinggi badan anak, lalu mengirimkan data tersebut ke server untuk dianalisis bersama data usia yang dimasukkan pengguna melalui web antarmuka GrowMyBaby.

## 🎯 Tujuan
Memberikan solusi deteksi dini stunting yang terjangkau, mudah digunakan, dan dapat diintegrasikan dengan sistem kesehatan berbasis web.

## 🔧 Komponen yang Digunakan
- **ESP32**
- **Sensor Load Cell + HX711** (untuk mengukur berat badan)
- **Sensor Ultrasonik HC-SR04** (untuk mengukur tinggi badan)
- **LCD I2C 16x2** (untuk menampilkan data)
- **Tombol Tekan** (untuk mengirim data)
- **LED Hijau dan Merah** (indikator status pengiriman)
- **Koneksi WiFi** (untuk menghubungkan ke server)

## 🖥️ Fitur Utama
- Pengukuran berat badan secara digital
- Pengukuran tinggi badan menggunakan sensor jarak
- Tampilan data di LCD
- Pengiriman data ke server melalui HTTP POST
- Indikator visual (LED) untuk keberhasilan/gagalnya pengiriman data

## 🔌 Cara Kerja
1. Perangkat membaca berat badan menggunakan HX711.
2. Perangkat membaca tinggi badan menggunakan sensor ultrasonik.
3. Data ditampilkan di LCD.
4. Saat tombol ditekan, data berat dan tinggi dikirim ke server.
5. LED hijau menyala jika data berhasil dikirim, LED merah jika gagal.
6. Usia anak dimasukkan melalui web interface.
7. Web server akan mengolah data berat, tinggi, dan usia untuk menilai status gizi anak.

## 🌐 Integrasi Web
- Endpoint server menerima data dalam format JSON:
  ```json
  {
    "weight": 3200.0,
    "height": 49.5
  }
  ```
- Usia anak dimasukkan secara manual di antarmuka web.
- Analisis dilakukan berdasarkan standar WHO untuk mendeteksi kemungkinan stunting.

##📦 Struktur Proyek
├── README.md
├── growmybaby.ino        # Kode utama mikrokontroler
└── (Web server terpisah) # Untuk menerima dan analisis data

##📝 Contoh Kode Penting
Koneksi WiFi
```c++
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED) {
  delay(1000);
  Serial.println("Connecting to WiFi...");
}
```

##Mengirim Data ke Server
```c++
String postData = "{\"weight\": " + String(weight) + ", \"height\": " + String(distance) + "}";
http.POST(postData);
```

##🚥 Indikator LED
- LED Hijau: Data berhasil dikirim ke server
- LED Merah: Gagal mengirim data atau WiFi tidak terhubung

##📌 Catatan
- Pastikan perangkat terhubung ke jaringan WiFi yang sama dengan server.
- Endpoint API server dapat diatur di variabel serverURL dalam kode.
- Kalibrasi sensor berat sangat penting agar hasil akurat.

##🤝 Kontribusi
Proyek ini masih dalam tahap prototipe. Masukan dan kontribusi sangat diterima untuk pengembangan lebih lanjut.

© 2025 GrowMyBaby Team
