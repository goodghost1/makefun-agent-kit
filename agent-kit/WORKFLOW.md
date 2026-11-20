# Workflow — cara membangun entry make.fun

Ini pipeline yang dijalankan untuk setiap bounty make.fun, ditulis supaya kamu bisa menjalankan pipeline yang sama dan supaya reviewer bisa melihat apa yang sebenarnya dilakukan. Ini ringkasan dari workflow yang berlaku, bukan salinannya.

## Pipeline-nya

```
Riset → Desain → Bangun → Verifikasi mandiri → Submit → Lacak
```

Untuk bug bounty klasik, tengahnya berubah menjadi `Audit → PoC → Verifikasi → Lapor → Submit`, tapi bentuknya sama: satu gerbang selesai sebelum gerbang berikutnya dimulai, dan tidak ada yang melewati gerbang.

| Tahap | Pekerjaan | Hasil |
|---|---|---|
| Riset | Cari bounty-nya, baca scope dan persyaratannya sampai habis. | Bounty + scope + apa yang masuk dan keluar + tenggat + biaya + penilaian. |
| Desain | Tuliskan apa yang akan dibangun, dengan urutan apa, dan seperti apa "selesai" itu. | Desain yang ditinjau pemilik sebelum build dimulai. |
| Bangun | Bangun di sesi yang terekam, dari desain itu. | Kode + README, ter-commit. |
| Verifikasi mandiri | Jalankan lagi setiap gerbang dan baca lagi kodenya, dengan bukti. | Lolos / lolos bersyarat / gagal, beserta buktinya. |
| Submit | Kirim lewat CLI kit, sesudah pemilik menyetujui preview-nya. | Submission ID + status. |
| Lacak | Awasi entry itu dan laporkan hanya ketika statusnya berubah. | Perubahan status, ke pemilik. |

## Aturan yang tidak pernah dilanggar

1. **Tidak ada data yang dikarang.** Setiap angka, tanggal, skor, peringkat, dan harga berasal dari sesuatu yang dibaca, dicek live, atau diukur. Kalau datanya tidak cukup, katakan "datanya tidak cukup" dan katakan apa yang kurang. Jangan pernah menyampaikan biaya atau batas yang belum terverifikasi sebagai fakta.
2. **Riset dulu.** Untuk game, pelajari dulu game nyata di genre itu — core loop-nya, kenapa ia seru — lalu rancang sesuatu yang orisinal dengan semangat yang sama. Jangan pernah mengkloning satu game tertentu.
3. **Bangun untuk menang, bukan untuk ikut-ikutan.** Setiap entry dibangun untuk bersaing di peringkat atas. Kalau dengan waktu dan sumber daya yang ada ia tidak bisa kompetitif, katakan begitu sebelum membangun, daripada mengirim entry pengisi.
4. **Dua kali tinjauan pemilik.** Desain ditinjau pemilik sebelum build dimulai, dan preview yang sudah jadi ditinjau pemilik sebelum submit. Submit hanya sesudah pemilik menyetujui preview-nya.
5. **Putusan verifikasi tidak bisa dibatalkan oleh koordinator.** Hanya pemilik yang bisa membatalkan putusan verifikasi, dan hanya dengan mengatakannya langsung.
6. **Rekam dengan bersih.** Selama rekaman berjalan, hanya lead dan builder yang aktif. Yang lain berhenti sampai segel selesai. Builder memeriksa recorder masih hidup sebelum setiap penulisan file.
7. **Versi baru dibangun di atas main.** Build ulang menimpa main; commit lama tetap ada di history dan SHA-nya tetap tercatat.
8. **Tidak ada pengeluaran tanpa perintah eksplisit.** Minting, penawaran, listing, transfer, dan biaya entry butuh perintah eksplisit pemilik yang menyebutkan koleksi, jumlah, chain, dan nominalnya.

## Aturan rekam / submit yang menggigit

- Sesi builder harus sesi top-level, dimulai oleh prompt pemilik sendiri, sesudah bounty dibuka. Build yang dilakukan subagent, atau yang diserahkan tanpa parent chat, gagal di gerbang run-record.
- System prompt dan file instruksi harus diunggah bersama entry. Menyembunyikannya adalah penolakan sejak 18 November 2026, 12:00 UTC.
- README harus ditulis dalam setidaknya dua pesan builder sendiri (draft, lalu revisi), dengan setidaknya 30% baris yang dihitung ditulis oleh agent di sesi yang diunggah.
- Jalankan `check` lokal sebelum `submit`. Submit yang ditolak tetap memakan kuota harian.
- Sesudah segel, mulai lagi semua yang dijeda, dan laporkan hasilnya.

## Pelajaran yang didapat dengan cara yang sulit

Pelajaran-pelajaran ini datang dari entry yang kalah dan submit yang gagal. Mereka bagian dari workflow, bukan catatan kaki.

- **Batas entry yang tertulis bukan batas yang sebenarnya.** Dua bounty berhenti di 3 entry padahal tertulis maksimal 20; submit keempat ditolak dengan HTTP 429 "entry quota reached" karena reputasi akun. Kirim sekali dengan versi terbaikmu, dan jangan pernah bilang revisi masih bisa masuk sampai platform sendiri yang menerimanya.
- **Revisi di bawah Force_Last adalah judi.** Submit baru membuang entry lama. Di dua bounty news-image, setiap revisi mendapat skor lebih rendah dari versi yang digantikannya. Revisi hanya kalau perubahannya jelas lebih baik, bukan sekadar beda.
- **Dev grade itu sinyal sementara, bukan peringkat final.** Dev grade datang dari 12 laga juri; final heat menilai ulang dari nol sesudah tenggat. Jangan membangun ulang mengikuti satu pola dari sampel kecil itu.
- **Verifikasi aturan sistemnya sebelum membangun.** Kuota, biaya, kriteria juri, cara transkrip dibaca — periksa di situsnya sendiri dulu, bukan dari ingatan.
- **Jangan pernah menjanjikan kemenangan.** Sampaikan peluang jujur dari data live: berapa entry, berapa tempat berbayar, dan di mana posisimu.
- **Jangan bakar entry untuk tes atau duplikat.** Setiap submit yang diterima dihitung ke kuota bounty itu. Uji dengan mock trial dan `check` lokal dulu; submit hanya versi terbaik.

## Loop lengkap, dari ujung ke ujung

Ini seluruh loop sebagaimana benar-benar berjalan, bukan sekadar nama-nama tahapnya.

**1. Cari dan triage.** Awasi bounty baru (papan make.fun, status watch). Untuk masing-masing, baca tugasnya, penilaiannya, tenggatnya, biayanya, dan file persyaratannya sampai habis — sebelum menulis apa pun. Triage berdasarkan data: hadiah lawan waktu yang tersisa, biaya lawan anggaran, kelayakan lawan skill dan perkakas yang ada. Keputusan go butuh alasan; no-go juga butuh alasan, ditulis. Jangan pernah memulai build pada bounty yang penilaiannya belum kamu baca.

**2. Riset.** Satu putaran yang menjawab: apa yang masuk scope, apa yang keluar, apa hasil yang diminta, apa yang akan diuji pemeriksaan, dan apa yang sudah menang di jenis bounty seperti ini. Untuk game, pelajari dulu game nyata di genre itu — core loop-nya, kenapa ia seru — lalu rancang sesuatu yang orisinal dengan semangat yang sama. Untuk audit, baca dulu kodenya dan petakan entry point sebelum berburu. Riset berakhir dengan putusan singkat: go, go dengan syarat, atau no-go, beserta angka-angka di baliknya.

**3. Desain.** Arsitek menulis desain selengkapnya: apa yang akan dibangun, dengan urutan apa, seperti apa "selesai" itu, apa trade-off-nya, dan apa yang akan dicek. Pemilik meninjau desain sebelum build apa pun dimulai. Trade-off yang belum dilihat pemilik bukan keputusan — itu kejutan, dan kejutan membuat entry ditolak.

**4. Bangun, di sesi yang terekam.** Builder bekerja di sesi top-level yang dimulai oleh prompt pemilik sendiri, sesudah bounty dibuka. Recorder harus hidup sebelum setiap penulisan file. Selama rekaman berjalan, hanya lead dan builder yang aktif — yang lain berhenti sampai segel. Versi baru dibangun di `main`; commit lama tetap ada di history. Builder menulis kode dan README dalam setidaknya dua pesannya sendiri, supaya gerbang revisi itu nyata, bukan dipentaskan.

**5. Verifikasi, secara mandiri.** Verifikasi menjalankan lagi setiap gerbang dan membaca lagi kodenya, dari nol, dengan bukti untuk setiap putusan: lolos, lolos bersyarat, atau gagal. Putusan verifikasi tidak pernah dibatalkan oleh koordinator — hanya pemilik yang bisa membatalkannya, dan hanya dengan mengatakannya langsung. Verifikasi yang gagal berarti entry tidak keluar, sedekat apa pun tenggatnya.

**6. Submit.** Kirim lewat CLI kit, sesudah pemilik menyetujui preview-nya. Catat submission ID dan statusnya. Jalankan `check` lokal dulu; submit yang ditolak tetap memakan kuota.

**7. Lacak.** Awasi status entry itu dan laporkan hanya ketika statusnya berubah: dev grade yang mendarat, hasil final, atau penolakan. Jangan menebak peringkat sebelum waktunya; dev grade bukan peringkat final.

## Cara memakai ulang workflow ini

Salin tabel pipeline dan delapan aturan ke catatanmu sendiri, dengan kata-katamu sendiri, di sesimu sendiri. Lalu jalankan satu bounty kecil melaluinya dari ujung ke ujung sebelum kamu mempercayainya untuk bounty besar. Pipeline itu baru nyata ketika sebuah putusan verifikasi benar-benar menghentikan entry yang buruk untuk keluar.
