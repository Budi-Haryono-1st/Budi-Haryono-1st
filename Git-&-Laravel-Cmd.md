## Laravel Local Installation
**Setup Project**
- run `git clone https://github.com/mauuas1st/bismillah.git`
- run `composer install`
- run `npm install`
- run `npm install vite --save-dev` (optional, when can't run npm run dev)
- run `npm run dev`

**Environment**
- run `cp .env.example .env`
- run `php artisan key:generate`
- set up your database in the `.env`

**Database & Storage**
- run `php artisan migrate --seed`
- run `php artisan storage:link`

**Run Server**
- run `php artisan serve`
- then visit `http://localhost:8000` atau `http://127.0.0.1:8000`

---

## Git & GitHub

### 🚀 First Time Setup (Komputer Baru)

**1. Install Git**

- **Windows** → download di [git-scm.com](https://git-scm.com), install, pakai Git Bash
- **Ubuntu** → `sudo apt update && sudo apt install git`

**2. Set Identity Global**
```bash
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"
```

**3. Buat SSH Key**
```bash
ssh-keygen -t ed25519 -C "email@kamu.com"
```
Tekan Enter terus sampai selesai.

**4. Tambah SSH Key ke ssh-agent**
```bash
# Windows (Git Bash) & Ubuntu
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**5. Copy Public Key → Daftarkan ke GitHub**
```bash
# Ubuntu
cat ~/.ssh/id_ed25519.pub

# Ubuntu (copy langsung ke clipboard)
xclip -selection clipboard < ~/.ssh/id_ed25519.pub
```
- Windows → buka file `C:\Users\NamaKamu\.ssh\id_ed25519.pub` pakai Notepad, copy semua isinya

Lalu di GitHub → **Settings → SSH and GPG Keys → New SSH Key** → paste → Save.

**6. Test Koneksi**
```bash
ssh -T git@github.com
# Harusnya muncul: Hi username!
```

---

### 📤 Push Project Baru ke GitHub (Pertama Kali)

**1. Buat repo baru di GitHub**
- Buka GitHub → klik **New Repository**
- Isi nama repo, jangan centang apapun (README, .gitignore) → **Create Repository**

**2. Di folder project kamu, jalankan:**
```bash
git init                          # inisialisasi git di folder
git add .                         # tambah semua file
git commit -m "first commit"      # commit pertama
git branch -M main                # rename branch ke main
git remote add origin git@github.com:username/nama-repo.git   # hubungkan ke GitHub
git push -u origin main           # push pertama kali
```

> Setelah `git push -u origin main`, berikutnya cukup pakai `git push` saja.

---

### 🖥️ 2 Akun GitHub di 1 Komputer

**Windows (Git Bash) & Ubuntu**

**1. Buat 2 SSH Key**
```bash
ssh-keygen -t ed25519 -C "email1@kamu.com" -f ~/.ssh/id_github_akun1
ssh-keygen -t ed25519 -C "email2@kamu.com" -f ~/.ssh/id_github_akun2
```

**2. Tambah ke ssh-agent**
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_github_akun1
ssh-add ~/.ssh/id_github_akun2
```

**3. Daftarkan ke masing-masing akun GitHub**
```bash
cat ~/.ssh/id_github_akun1.pub   # copy → paste ke akun 1
cat ~/.ssh/id_github_akun2.pub   # copy → paste ke akun 2
```
GitHub → **Settings → SSH and GPG Keys → New SSH Key**

**4. Buat SSH Config**
```bash
nano ~/.ssh/config
```
Isi:
```
# Akun 1
Host github-akun1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_akun1

# Akun 2
Host github-akun2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_akun2
```
Simpan `Ctrl+X → Y → Enter`. Khusus Ubuntu tambah:
```bash
chmod 600 ~/.ssh/config
```

**5. Set Remote per Project**
```bash
# Project akun 1
git remote set-url origin git@github-akun1:username1/nama-repo.git

# Project akun 2
git remote set-url origin git@github-akun2:username2/nama-repo.git
```

**6. Set Identity per Project (lokal)**
```bash
git config user.name "Nama Akun 1"
git config user.email "email1@kamu.com"
```

**7. Test Koneksi**
```bash
ssh -T git@github-akun1   # Hi username1!
ssh -T git@github-akun2   # Hi username2!
```

---

### Update Github
- `git pull` → ambil update terbaru dari remote
- `git add .` → tambah semua file ke staging
- `git add namafile` → tambah file tertentu
- `git status` → lihat perubahan file
- `git commit -m "pesan"` → simpan perubahan
- `git commit -am "pesan"` → add + commit (hanya file yang sudah tracked)
- `git push` → kirim ke repository
- `git push origin namabranch` → push ke branch tertentu

---

### 🌿 Branching
- `git branch` → lihat branch lokal
- `git branch -r` → lihat branch remote
- `git branch namabranch` → buat branch baru
- `git checkout namabranch` → pindah branch
- `git switch namabranch` → pindah branch (versi baru)
- `git switch -c namabranch` → buat + pindah branch
- `git merge namabranch` → gabung branch ke branch aktif
- `git branch -d namabranch` → hapus branch lokal

---

### 📦 Stash

**Simpan perubahan sementara**
- `git stash` → simpan perubahan sementara
- `git stash list` → lihat daftar stash
- `git stash apply` → pakai kembali stash
- `git stash pop` → pakai + hapus stash
- `git stash drop` → hapus stash tertentu
- `git stash clear` → hapus semua stash

---

### 👤 Git Config

**🔍 Melihat config**
- `git config --global user.name` → lihat username
- `git config --global user.email` → lihat email
- `git config --list` → lihat semua config

**➕ Menambahkan / mengubah**
- `git config --global user.name "Nama Kamu"`
- `git config --global user.email "email@kamu.com"`

**⚙️ Khusus repo saja (tanpa --global)**
- `git config user.name "Nama Kamu"`
- `git config user.email "email@kamu.com"`

---

### 🔗 Remote Repository
- `git remote -v` → lihat remote repo
- `git remote add origin URL` → tambah repo
- `git remote remove origin` → hapus remote
- `git push -u origin main` → push pertama kali

---

### 🔄 Undo / Perbaikan
- `git restore namafile` → kembalikan file
- `git reset namafile` → hapus dari staging
- `git reset --hard` → reset semua perubahan ⚠️ hati-hati
- `git revert HEAD` → batalkan commit terakhir (aman)

---

### 📜 Log & History
- `git log` → lihat history commit
- `git log --oneline` → versi ringkas
- `git diff` → lihat perubahan
- `git diff --staged` → lihat perubahan yang sudah di-add

---

### 🧹 Clean
- `git clean -fd` → hapus file yang tidak ter-track
