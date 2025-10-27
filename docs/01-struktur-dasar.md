# 📘 **Struktur Dasar EA Setelah Generate File Baru di MQL5**

Saat kamu membuat EA baru lewat MetaEditor → *New → Expert Advisor (template)*, otomatis akan muncul kerangka kode seperti ini:

```mql5
//+------------------------------------------------------------------+
//|                                             MyExpertAdvisor.mq5 |
//|                        Copyright 2025, Nama Kamu                |
//|                                             https://www.mql5.com |
//+------------------------------------------------------------------+
#property copyright "Copyright 2025 Nama Kamu"
#property link      "https://www.mql5.com"
#property version   "1.00"
#property strict

//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
int OnInit()
{
   // Kode yang dijalankan saat EA pertama kali diaktifkan
   return(INIT_SUCCEEDED);
}

//+------------------------------------------------------------------+
//| Expert deinitialization function                                 |
//+------------------------------------------------------------------+
void OnDeinit(const int reason)
{
   // Kode yang dijalankan saat EA dihentikan
}

//+------------------------------------------------------------------+
//| Expert tick function                                             |
//+------------------------------------------------------------------+
void OnTick()
{
   // Kode utama EA dijalankan di sini (setiap ada pergerakan harga)
}
//+------------------------------------------------------------------+
```

---

## ✅ **Penjelasan Struktur Ini Bagian per Bagian**

### 📌 1. **Header / Informasi File**

```mql5
//|                                             MyExpertAdvisor.mq5 |
//|                        Copyright 2025, Nama Kamu                |
#property copyright "..."
#property link      "..."
#property version   "1.00"
#property strict
```

| Baris               | Fungsi                                                       |
| ------------------- | ------------------------------------------------------------ |
| `#property version` | Menunjukkan versi EA kamu (contoh: 1.00, 1.01, v1.0-alpha)   |
| `#property link`    | Bisa diisi website kamu / GitHub / kosong                    |
| `#property strict`  | Mode ketat supaya penulisan kode lebih aman (wajib dipakai!) |

---

### 📌 2. **Fungsi `OnInit()` – Saat EA Baru Dipasang**

```mql5
int OnInit()
{
   return(INIT_SUCCEEDED);
}
```

✔ Dipanggil **sekali saja** saat EA dipasang di chart.
✔ Tempat untuk *setup awal*, seperti:

* Inisialisasi variabel
* Menyiapkan indikator
* Menampilkan pesan “EA siap digunakan”

---

### 📌 3. **Fungsi `OnTick()` – Otak Utama EA**

```mql5
void OnTick()
{
   // Di sini tempat EA berpikir & mengambil keputusan trading
}
```

✔ Dipanggil **setiap kali harga berubah (tick masuk)**
✔ Semua logika EA (Buy/Sell, cek sinyal, money management) ada di sini.
✔ Contohnya:

```mql5
double ask = SymbolInfoDouble(_Symbol, SYMBOL_ASK);
```

---

### 📌 4. **Fungsi `OnDeinit()` – Saat EA Dihapus atau Chart Ditutup**

```mql5
void OnDeinit(const int reason)
{
   // Membersihkan objek, menutup file log, dll
}
```

✔ Panggilan terakhir sebelum EA mati.
✔ Bisa digunakan untuk:

* Membersihkan grafik/objek
* Menutup file
* Mengetahui alasan EA dimatikan (manual/offline/reload)

---

## ✅ **Flow Kerja EA Secara Sederhana**

```
EA di-attach ke chart
        ↓
OnInit()  → persiapan
        ↓
OnTick() → berjalan terus menerus selama market bergerak
        ↓
OnDeinit() → saat EA dihentikan
```

---

## 🎯 **Jadi singkatnya:**

| Fungsi       | Kapan berjalan                     | Untuk apa?                    |
| ------------ | ---------------------------------- | ----------------------------- |
| `OnInit()`   | Saat EA baru dijalankan            | Persiapan                     |
| `OnTick()`   | Terus-menerus setiap harga berubah | Logika utama trading          |
| `OnDeinit()` | Saat EA dimatikan                  | Bersih-bersih & tutup program |

---
