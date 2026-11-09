# Catatan Workshop: From AI to GitHub

**Judul:** Building with AI, Managing Change with GitHub
**Pemateri:** Nugi Farhan, Senior Product Designer (6 tahun pengalaman; UX Advisor Bangkit, DBS CodingCamp, BI Hackathon)

---

## 1. Materi yang Disampaikan

| No | Topik |
|----|-------|
| 1 | Tujuan pembelajaran (capaian) |
| 2 | Prompt Engineering |
| 3 | Pengenalan Git dan alur kerjanya (Git Workflow) |
| 4 | Perbedaan Git dan GitHub |
| 5 | Perintah dasar Git dan Git ke GitHub |
| 6 | Setup Git, VS Code, dan SSH Key |
| 7 | Praktik: membuat Student Task Planner dengan AI lalu mengelolanya di GitHub |

### Capaian Pembelajaran

- Dapat menjelaskan bagaimana prompt AI yang lebih spesifik menghasilkan hasil yang lebih baik.
- Dapat membedakan Git dan GitHub.
- Dapat mengidentifikasi repository, commit, branch, dan pull request.
- Dapat melakukan version controlling.

---

## 2. Rangkuman Materi

### 2.1 Prompt Engineering

**Prompt** adalah instruksi atau masukan yang diberikan kepada model AI untuk mendapatkan hasil tertentu. Bentuknya bisa berupa pertanyaan sederhana, kata kunci, instruksi rumit, atau potongan kode.

**Prompt Engineering** adalah cara merancang instruksi agar AI memberikan jawaban yang tepat, relevan, dan layak digunakan.

**Konteks adalah kunci.**

- Tanpa konteks: `Create student task planner`
- Dengan konteks: prompt yang menjelaskan peran, tujuan, kebutuhan, batasan, dan format keluaran. Hasilnya jauh lebih terarah.

**Struktur prompt yang baik:**

| Elemen | Fungsi | Contoh dari slide |
|--------|--------|-------------------|
| Role | Menentukan peran AI | "You are helping me build a beginner-friendly student task planner..." |
| Task | Menjelaskan tujuan utama | "Create a task planner that helps first-year university students..." |
| Context | Kebutuhan dan batasan | Requirements (daftar fitur) dan Constraints (HTML, CSS, vanilla JS, tanpa library tambahan) |
| Format | Bentuk hasil yang diminta | "Provide the complete code for each file, explain how to run the application..." |

Ada juga instruksi penutup yang penting: *"Do not claim that the application works until you have verified its behavior."* Ini mengingatkan AI agar tidak mengklaim hasilnya benar sebelum diverifikasi.

**Taktik menulis prompt (sumber: Google Cloud):**

- Gunakan kata kerja aksi untuk menentukan tindakan yang diinginkan.
- Tentukan panjang dan format keluaran.
- Sebutkan target audiens.
- Sertakan fakta dan data yang relevan.
- Rujuk sumber atau dokumen tertentu.
- Definisikan istilah dan konsep kunci.

**Keuntungan prompt engineering:**

- Meningkatkan performa model AI.
- Mengurangi bias dan respons yang ofensif.
- Meningkatkan kontrol dan prediktabilitas.
- Memberikan pengalaman yang lebih baik.

### 2.2 Apa itu Git?

Git adalah *version control system* yang melacak siapa, kapan, dan apa saja yang diubah dalam suatu file. Git diciptakan oleh Linus Torvalds pada tahun 2005.

### 2.3 Git Workflow

Ada tiga area utama di Git:

1. **Working directory (working tree):** salinan satu versi proyek yang sedang dikerjakan, tempat file diubah.
2. **Staging area (index):** tempat menyimpan informasi tentang perubahan yang akan masuk ke commit berikutnya.
3. **Git directory (repository, folder `.git`):** tempat Git menyimpan metadata dan object database proyek. Bagian inilah yang disalin saat melakukan `clone`.

Alurnya: **Working Directory → (stage fixes) → Staging Area → (commit) → Repository.** Perintah *checkout* membawa versi proyek dari repository ke working directory.

### 2.4 Git vs GitHub

| | Git | GitHub |
|---|-----|--------|
| Jenis | Sistem version control terdistribusi (DVCS) | Platform berbasis web |
| Fungsi | Melacak dan mengelola perubahan kode secara lokal | Menyimpan repository Git secara online dan mendukung kolaborasi |

Singkatnya: Git adalah alatnya, GitHub adalah tempat menyimpan dan berkolaborasi.

### 2.5 Perintah Dasar

```bash
git init                      # Memulai repo baru
git add .                     # Memindahkan file ke staging area
git commit -m "message"       # Menyimpan perubahan ke repository

git remote add origin <url>   # Menghubungkan repo lokal ke repo di GitHub
git push origin main          # Mengirim branch saat ini ke remote
git pull origin main          # Mengambil perubahan lalu menggabungkannya ke branch saat ini
git clone "url"               # Menyalin repo dari GitHub ke komputer
```

**Variasi `git add`:**

| Perintah | Keterangan |
|----------|------------|
| `git add --all` / `git add -A` | Perilakunya sama, menambahkan semua perubahan di repository ke staging area |
| `git add .` | Menambahkan semua file di direktori saat ini beserta isinya |
| `git add *` | Menambahkan file yang dimodifikasi atau baru, tetapi tidak file yang dihapus |

Dua cara menambahkan repository ke Git:

1. `git init` di folder proyek lokal, atau
2. Buat repository baru di GitHub, klik tombol **Code**, salin link di tab Local, lalu jalankan `git clone "url"` di terminal.

### 2.6 Setup yang Dipelajari

**Git**

1. Install Git, pilih versi sesuai perangkat.
2. Cek dengan `git --version`.
3. Atur identitas:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   ```
4. Cek konfigurasi dengan `git config --global --list`.

**VS Code**

1. Install VS Code.
2. Tekan `Cmd/Ctrl + Shift + P`, cari *Shell Command: Install 'code' command in PATH*.
3. Cek dengan `code --version`.

**SSH Key untuk GitHub**

```bash
# 1. Buat SSH key
ssh-keygen -t ed25519 -C "email@domain.com"
# Tekan Enter untuk lokasi default; isi passphrase (atau Enter dua kali tanpa passphrase)

# 2. Jalankan SSH agent
eval "$(ssh-agent -s)"

# 3. Buat atau edit ~/.ssh/config, lalu isi:
#   Host github.com
#     AddKeysToAgent yes
#     UseKeychain yes
#     IdentityFile ~/.ssh/id_ed25519
touch ~/.ssh/config

# 4. Tambahkan key ke agent (macOS Keychain)
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# 5. Salin public key
pbcopy < ~/.ssh/id_ed25519.pub
```

Lalu di GitHub: **Settings → SSH and GPG keys → New SSH key**, isi Title (misalnya "MacBook"), biarkan Key type sebagai *Authentication Key*, tempel key, klik **Add SSH key**.

Verifikasi koneksi:

```bash
ssh -T git@github.com
# Hasil: Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

Tentang **Ed25519:** *Ed* berarti EdDSA (Edwards-curve Digital Signature Algorithm), sedangkan *25519* merujuk pada kurva Curve25519 (dibuat tahun 2011 oleh Daniel J. Bernstein). Skema tanda tangan ini dirancang untuk keamanan dan performa tinggi serta tahan terhadap serangan implementasi umum.

**Checklist setup:**

```bash
git --version
git config --global user.name
git config --global user.email
code --version
ssh -T git@github.com
```

### 2.7 Praktik: Student Task Planner

Proyek sederhana berupa aplikasi web pencatat tugas untuk mahasiswa baru. Fitur yang diminta pada prompt:

- Menampilkan daftar tugas contoh (judul, tenggat, status selesai).
- Menandai tugas sebagai selesai.
- Filter: semua, pending, dan selesai.
- Tampilan bersih, mudah dibaca, dan responsif.
- Teknologi: HTML, CSS, dan vanilla JavaScript.

**Alur kerja praktik:**

1. Gunakan platform AI (Claude, Antigravity, ChatGPT).
2. Tulis prompt untuk membuat web/aplikasi.
3. `git init` untuk menambahkannya ke Git.
4. Commit lalu push ke GitHub.
5. Lakukan perubahan.
6. Commit dan push lagi ke GitHub.

---

## 3. Poin Penting dan Pengetahuan Baru

- Prompt yang spesifik (peran, tugas, konteks, format) menghasilkan keluaran AI yang lebih akurat dan siap pakai daripada prompt singkat.
- Meminta AI memverifikasi hasilnya sebelum mengklaim berhasil adalah praktik yang baik.
- Git bekerja lokal dan mencatat riwayat perubahan; GitHub menyimpannya online untuk kolaborasi. Keduanya bukan hal yang sama.
- Perubahan melewati tiga tahap: working directory, staging area, lalu repository. Commit hanya menyimpan apa yang sudah di-stage.
- Setup identitas (`user.name`, `user.email`) wajib dilakukan agar setiap commit tercatat siapa yang membuatnya.
- SSH key membuat koneksi ke GitHub aman tanpa perlu memasukkan kredensial setiap kali push atau pull.
- Alur dasar yang diulang terus: **ubah → `git add` → `git commit` → `git push`**.
- Commit yang sering dan pesan commit yang jelas memudahkan penelusuran riwayat dan kolaborasi.
