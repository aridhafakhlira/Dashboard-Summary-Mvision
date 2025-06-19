# Dashboard Summary Mvision
![Judul](judul.png)


## Pendahuluan
Proyek **"Dashboard Summary Mvision"** dikembangkan untuk memenuhi kebutuhan esensial bisnis dalam memantau dan mengukur kinerja operasional secara kuantitatif melalui Key Performance Indicator (KPI) yang relevan. Dashboard ini berfungsi sebagai pusat informasi interaktif bagi para pemangku kepentingan untuk mendapatkan wawasan cepat mengenai metrik-metrik operasional kunci.

## Kebutuhan Bisnis
Dalam lingkungan bisnis yang dinamis, kemampuan untuk memantau kinerja secara real-time adalah krusial. Dashboard ini dibangun untuk mengatasi kebutuhan berikut:
- Memberikan visibilitas yang jelas terhadap metrik operasional utama.
- Membantu pengambilan keputusan berbasis data yang lebih cepat dan tepat.
- Mengidentifikasi tren dan anomali dalam data pelanggan dan keuangan.

## Solusi: Dashboard Interaktif di Metabase
Kami membangun dashboard interaktif menggunakan **Metabase** yang menyajikan serangkaian KPI penting untuk memberikan gambaran komprehensif tentang performa bisnis. Dashboard ini dirancang agar mudah dipantau berbagai pemangku kepentingan.

### Metrik yang Disajikan
Dashboard ini menampilkan berbagai metrik vital, termasuk:
- **Total Jumlah Pelanggan Aktif:** Perbandingan jumlah pelanggan aktif hari ini dan kemarin untuk melacak pertumbuhan atau penurunan harian.
- **Total Pelanggan Aktif (Prepaid vs. Postpaid):** Insight terperinci mengenai jumlah pelanggan aktif berdasarkan tipe langganan (prabayar dan pascabayar) per hari ini dan kemarin.
- **Total Pelanggan Prediksi:** Memantau jumlah pelanggan yang diprediksi berdasarkan model tertentu (misal prediksi churn, prediksi penggunaan layanan).
- **Total Amount Collection Bulanan:** Agregasi total pendapatan yang berhasil dikumpulkan setiap bulan, penting untuk analisis keuangan.
- **Jumlah Subs Aktif Harian:** Tren jumlah langganan (subs) yang aktif setiap harinya.
- **Jumlah Amount Harian:** Tren total pendapatan yang dikumpulkan setiap hari.
- **Pelanggan Disconnect:** Metrik jumlah pelanggan yang menghentikan layanan.
- **Pelanggan Melakukan Pembayaran:** Metrik jumlah pelanggan yang berhasil melakukan pembayaran dalam periode tertentu.

## Alat & Teknologi
Proyek ini memanfaatkan kombinasi alat dan teknologi berikut untuk ekstraksi data, pemrosesan, dan visualisasi:
- **SQL:** Digunakan untuk menulis query yang kompleks guna mengekstrak dan memanipulasi data dari database.
- **Oracle Database:** Sistem manajemen basis data tempat data operasional disimpan dan diakses.
- **Metabase:** Platform Business Intelligence (BI) open-source yang digunakan untuk membangun dashboard interaktif, visualisasi data, dan berbagi wawasan.

## Metodologi
Proses pengembangan dashboard melibatkan langkah-langkah berikut:
1. **Pengambilan Data:** Data mentah diekstraksi langsung dari Oracle Database menggunakan query SQL spesifik.
2. **Transformasi Data (SQL):** Query SQL ditulis untuk membersihkan, menggabungkan, dan mengubah data sesuai kebutuhan metrik—termasuk agregasi harian, bulanan, serta pengelompokan berdasarkan kategori (misal prepaid/postpaid).
3. **Koneksi Metabase:** Metabase dikonfigurasi untuk terhubung ke Oracle Database, memungkinkan akses langsung ke tabel dan view yang relevan.
4. **Desain Dashboard:** Di Metabase, pertanyaan (queries) dibangun dan visualisasi (grafik, tabel, KPI cards) dibuat untuk merepresentasikan metrik yang diinginkan.
5. **Penyusunan Dashboard:** Visualisasi-visualisasi ini kemudian disusun ke dalam sebuah dashboard interaktif yang mudah dinavigasi.

## Hasil Visualisasi
Berikut adalah contoh tampilan dashboard Summary Mvision yang telah dibangun:

![image1](image1)

## Contoh Source Code SQL (View)
Salah satu contoh query SQL yang digunakan untuk ekstraksi dan transformasi data pada dashboard:

```sql
SELECT
  *
FROM
  (
    SELECT
      "source"."TGL_REPORT" "TGL_REPORT",
      "source"."FLAG" "FLAG",
      "source"."TOTAL_SUBS" "TOTAL_SUBS"
    FROM
      (
        select
          tgl_report,
          'Paying Subs' FLAG,
          sum(TOTAL_SUBS) Total_SUBS
        from
          prod.F_SUMMARY_NETADD_MVISION
        where
          urutan in(4, 5)
          and trunc(tgl_report) in(trunc(sysdate -1), trunc(sysdate -2))
        group by
          tgl_report
      ) "source"
  )
WHERE
  rownum <= 1048575
```

---

_Portofolio ini memberikan gambaran bagaimana dashboard Summary Mvision dibangun dan diimplementasikan untuk kebutuhan pemantauan kinerja bisnis secara real-time dan komprehensif._
