# 🎵 Free Music for Symphony

Fitur **Free Music** adalah modul tambahan untuk aplikasi **Symphony** yang secara otomatis mengunduh beberapa lagu gratis saat aplikasi pertama kali dijalankan. Tujuannya adalah agar pengguna langsung bisa mencoba pemutar musik tanpa perlu menambahkan file secara manual terlebih dahulu.

---

## ✨ Fitur Utama
- ✅ Mengunduh lagu bawaan dari internet pada saat **first launch**.  
- ✅ Lagu disimpan di **folder publik Music/Symphony**, sehingga bisa diakses juga oleh aplikasi musik lain.  
- ✅ Mendukung **DownloadManager** Android dengan notifikasi progress.  
- ✅ **Auto-rescan MediaStore** setelah selesai agar lagu langsung tampil di library Symphony.  
- ✅ Hanya berjalan **sekali saja**, tidak akan mengulang setelah sukses.  

---

## 📂 Struktur Folder
File musik hasil unduhan disimpan ke: /storage/emulated/0/Music/Symphony/
```
Music/
└── Symphony/
├── song1.mp3
├── song2.mp3
└── song3.mp3
```
---

## ⚙️ Cara Kerja
1. Saat `MainActivity` dijalankan, dipanggil `startDefaultDownloads()`.  
2. Kelas [`DefaultSongDownloader`](app/src/main/java/io/github/zyrouge/symphony/DefaultSongDownloader.kt) akan:
   - Mengecek apakah sudah pernah download (pakai `SharedPreferences`).  
   - Jika belum, maka `DownloadManager` mengunduh daftar URL di `DefaultSongs.urls`.  
   - Saat semua download selesai → ditandai `done = true` agar tidak mengulang.  
   - Trigger **media scan** supaya lagu terdeteksi oleh library musik.  

---

## 🔑 Permission
Karena file musik disimpan di folder publik, aplikasi memerlukan izin:

- Android 13+ (`SDK 33+`):  
  - `READ_MEDIA_AUDIO`
- Android 12 dan di bawahnya:  
  - `READ_EXTERNAL_STORAGE`

Aplikasi otomatis meminta izin ini saat pertama kali dijalankan.  

---

## 📝 Konfigurasi Lagu Default
Daftar URL lagu default didefinisikan di file: DefaultSongs.kt

Contoh:

```kotlin
object DefaultSongs {
    val urls = listOf(
        "https://raw.githubusercontent.com/username/free-music-symphony/main/audio/lagu1.mp3",
        "https://raw.githubusercontent.com/username/free-music-symphony/main/audio/lagu2.mp3",
        "https://raw.githubusercontent.com/username/free-music-symphony/main/audio/lagu3.mp3"
    )
}
```
---

## ⚠️ Pastikan file yang digunakan bebas hak cipta (royalty-free / creative commons).

---

## 📌 Catatan

Jika user menolak izin, unduhan tetap berjalan, tapi aplikasi mungkin tidak bisa langsung membaca file.

Pada beberapa device, media scan otomatis sudah bekerja, tapi broadcast tambahan tetap dikirim untuk kompatibilitas.

Fitur ini opsional, pengguna tetap bisa menambahkan musik mereka sendiri.

---

## 📜 Lisensi Musik

Lagu bawaan harus bersumber dari musik dengan lisensi:

Royalty-Free

Creative Commons (CC0 / CC-BY)

Atau musik open-source lain yang legal untuk distribusi

Harap sertakan kredit (jika lisensi mengharuskan).

---

## 👨‍💻 Kontributor

Fitur ini dikembangkan sebagai bagian dari modifikasi project Symphony untuk memberikan pengalaman pertama yang lebih baik bagi pengguna baru.

---

