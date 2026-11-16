# Hidayah — Game Edukasi Islami (Java 2D)

**Hidayah** adalah game RPG 2D bertema Islami. Pemain menjelajahi dunia,
berinteraksi dengan NPC, dan menjawab **kuis seputar ajaran Islam**
(rukun Islam, shalat, zakat, puasa, haji) untuk mengumpulkan skor.
Skor tertinggi tiap pemain tersimpan di **leaderboard** (MySQL).

> Tugas kelompok — **Kelompok 1**.

## Teknologi
- **Java** (Swing/AWT) — digambar manual via `Graphics2D`, game loop 60 FPS
- **MySQL / MariaDB** (JDBC) — penyimpanan leaderboard
- Dikembangkan dengan **Eclipse**

## Kontrol
| Tombol | Aksi |
|--------|------|
| `W` `A` `S` `D` / panah | Bergerak |
| `Shift` | Lari |
| `Enter` | Interaksi / pilih menu |

## Cara Menjalankan

### Prasyarat
- **JDK 21** (atau yang kompatibel)
- *(Opsional)* **MySQL/MariaDB** + **MySQL Connector/J** — hanya untuk leaderboard

### A. Lewat terminal
```bash
cd Hidayah

# Compile
javac -d bin $(find src -name "*.java")

# Jalankan (tanpa leaderboard)
java -cp "bin:res" main.Main

# Jalankan dengan leaderboard (butuh JAR MySQL, lihat Hidayah/lib/README.md)
java -cp "bin:res:lib/mysql-connector-j.jar" main.Main
```
> Windows: ganti pemisah classpath `:` menjadi `;`.

### B. Lewat Eclipse
1. Import folder `Hidayah` sebagai project.
2. Taruh `mysql-connector-j.jar` di `Hidayah/lib/` (lihat [lib/README.md](Hidayah/lib/README.md)).
3. Run `src/main/Main.java` sebagai Java Application.

## Setup Database (opsional, untuk leaderboard)
1. Jalankan MySQL (mis. lewat XAMPP) dan buka phpMyAdmin.
2. Import file [`game_database.sql`](game_database.sql) — membuat database `game_database` berisi tabel `leaderboard`.
3. Konfigurasi koneksi ada di [`Hidayah/src/main/FileManager.java`](Hidayah/src/main/FileManager.java)
   (default: host `localhost:3306`, user `root`, password kosong — sesuaikan bila perlu).

## Catatan
- **File audio tidak disertakan** di repo (ukuran besar & hak cipta). Game tetap
  jalan tanpa suara. Untuk menambah audio, lihat [res/sound/README.md](Hidayah/res/sound/README.md).
- **JAR MySQL tidak disertakan**; download sendiri — lihat [lib/README.md](Hidayah/lib/README.md).

## Struktur Project
```
Hidayah/src/
├── main/     Inti game: Main, GamePanel, KeyHandler, UI, Sound, FileManager, ...
├── entity/   Player, Entity, NPC, dan "Buku" pemicu kuis
├── quiz/     Quiz + quizOne/Two/Three (bank soal)
├── object/   Benda dunia: kunci, diploma, kursi, dll.
└── tile/     Sistem peta berbasis tile
Hidayah/res/  Aset: tiles, player, npc, objects, maps, font (sound menyusul)
game_database.sql   Skema + data awal leaderboard
```
