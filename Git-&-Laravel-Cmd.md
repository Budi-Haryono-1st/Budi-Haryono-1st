# 📘 Dokumentasi Developer
> Laravel · Git · GitHub

---

## 🚀 Laravel Local Installation

### Setup Project

```bash
git clone https://github.com/mauuas1st/bismillah.git
composer install
npm install
npm install vite --save-dev   # opsional, ketika tidak bisa npm run dev
npm run dev
```

### Environment

```bash
cp .env.example .env
php artisan key:generate
```

> Set up database kamu di file `.env`

### Database & Storage

```bash
php artisan migrate --seed
php artisan storage:link
```

### Run Server

```bash
php artisan serve
```

> Kunjungi `http://localhost:8000` atau `http://127.0.0.1:8000`

---

## 🛠️ Git & GitHub

### 🚀 First Time Setup (Komputer Baru)

**1. Install Git**

- **Windows** → download di [git-scm.com](https://git-scm.com), install, pakai Git Bash
- **Ubuntu**

```bash
sudo apt update && sudo apt install git
```

**2. Set Identity Global**

```bash
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"
```

**3. Buat SSH Key**

```bash
ssh-keygen -t ed25519 -C "email@kamu.com"
```

> Tekan Enter terus sampai selesai.

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

> **Windows** → buka file `C:\Users\NamaKamu\.ssh\id_ed25519.pub` pakai Notepad, copy semua isinya

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

### 🖥️ 2 Menambahkan 2 Akun GitHub di Ubuntu

**Ubuntu**

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

> GitHub → **Settings → SSH and GPG Keys → New SSH Key**

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

> Simpan `Ctrl+X → Y → Enter`. Khusus Ubuntu tambah:

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

### 🖥️ Menambahkan 2 Akun GitHub di Windows

***Windows (Powwershell "administrator")***

**1. Aktifkan ssh-agent**

```powershell
Get-Service ssh-agent
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
```

**2. Buat 2 SSH Key**

```powershell
ssh-keygen -t ed25519 -C "email_1@kamu.com"
# Simpan ke: C:\Users\Admin\.ssh\id_ed25519_budi

ssh-keygen -t ed25519 -C "email_2@kamu.com"
# Simpan ke: C:\Users\Admin\.ssh\id_ed25519_mauuas
```

> Pastikan hasilnya seperti ini:
> ```
> Your identification has been saved in C:\Users\Admin\.ssh\id_ed25519_mauuas
> Your public key has been saved in C:\Users\Admin\.ssh\id_ed25519_mauuas.pub
> The key fingerprint is:
> SHA256:uwBPH/er6YYYF6I/I9xQ97/JWAqpoljkmPSWYki4TtZnw email_2@kamu.com
> ```

**3. Verifikasi file SSH**

```powershell
dir C:\Users\Admin\.ssh
```

> Pastikan ada file `id_ed25519_budi`, `id_ed25519_budi.pub`, `id_ed25519_mauuas`, `id_ed25519_mauuas.pub`

**4. Tambah Key ke ssh-agent**

```powershell
ssh-add C:\Users\Admin\.ssh\id_ed25519_budi
# Identity added: C:\Users\Admin\.ssh\id_ed25519_budi (email_1@kamu.com)

ssh-add C:\Users\Admin\.ssh\id_ed25519_mauuas
# Identity added: C:\Users\Admin\.ssh\id_ed25519_mauuas (email_2@kamu.com)
```

**5. Copy Public Key ke GitHub**

```powershell
type C:\Users\Admin\.ssh\id_ed25519_budi.pub
# copy output → paste ke SSH di GitHub akun 1

type C:\Users\Admin\.ssh\id_ed25519_mauuas.pub
# copy output → paste ke SSH di GitHub akun 2
```

**6. Edit SSH Config**

```powershell
notepad C:\Users\Admin\.ssh\config
```

> Jika tidak bisa via CMD, akses lewat Explorer di: `C:\Users\Admin\.ssh\config`

Tambahkan isi berikut:

```
# Akun Budi
Host github-budi
  HostName github.com
  User git
  IdentityFile C:\Users\Admin\.ssh\id_ed25519_budi

# Akun Mauuas
Host github-mauuas
  HostName github.com
  User git
  IdentityFile C:\Users\Admin\.ssh\id_ed25519_mauuas
```

**7. Set Remote per Project**

```bash
# Project akun 1
git remote set-url origin git@github-akun1:username1/nama-repo.git

# Project akun 2
git remote set-url origin git@github-akun2:username2/nama-repo.git
```

**8. Set Identity per Project (lokal)**

```bash
git config user.name "Nama Akun 1"
git config user.email "email1@kamu.com"
```

**9. Test Koneksi**

```powershell
ssh -T git@github-budi
# Hi Budi-Haryono-1st! You've successfully authenticated, but GitHub does not provide shell access.

ssh -T git@github-mauuas
# Hi mauuas1st! You've successfully authenticated, but GitHub does not provide shell access.
```

> Jika muncul peringatan `The authenticity of host 'github.com' can't be established`, ketik `yes` untuk melanjutkan.

---

### 🔄 Update GitHub

```bash
git pull                         # ambil update terbaru dari remote
git add .                        # tambah semua file ke staging
git add namafile                 # tambah file tertentu
git status                       # lihat perubahan file
git commit -m "pesan"            # simpan perubahan
git commit -am "pesan"           # add + commit (hanya file yang sudah tracked)
git push                         # kirim ke repository
git push origin namabranch       # push ke branch tertentu
```

---

### 🌿 Branching

```bash
git branch                       # lihat branch lokal
git branch -r                    # lihat branch remote
git branch namabranch            # buat branch baru
git checkout namabranch          # pindah branch
git switch namabranch            # pindah branch (versi baru)
git switch -c namabranch         # buat + pindah branch
git merge namabranch             # gabung branch ke branch aktif
git branch -d namabranch         # hapus branch lokal
```

---

### 📦 Stash

```bash
git stash                        # simpan perubahan sementara
git stash list                   # lihat daftar stash
git stash apply                  # pakai kembali stash
git stash pop                    # pakai + hapus stash
git stash drop                   # hapus stash tertentu
git stash clear                  # hapus semua stash
```

---

### 👤 Git Config

**🔍 Melihat config**

```bash
git config --global user.name    # lihat username
git config --global user.email   # lihat email
git config --list                # lihat semua config
```

**➕ Menambahkan / mengubah**

```bash
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"
```

**⚙️ Khusus repo saja (tanpa --global)**

```bash
git config user.name "Nama Kamu"
git config user.email "email@kamu.com"
```

---

### 🔗 Remote Repository

```bash
git remote -v                    # lihat remote repo
git remote add origin URL        # tambah repo
git remote remove origin         # hapus remote
git push -u origin main          # push pertama kali
```

---

### 🔄 Undo / Perbaikan

```bash
git restore namafile             # kembalikan file
git reset namafile               # hapus dari staging
git reset --hard                 # reset semua perubahan ⚠️ hati-hati
git revert HEAD                  # batalkan commit terakhir (aman)
```

---

### 📜 Log & History

```bash
git log                          # lihat history commit
git log --oneline                # versi ringkas
git diff                         # lihat perubahan
git diff --staged                # lihat perubahan yang sudah di-add
```

---

### 🧹 Clean

```bash
git clean -fd                    # hapus file yang tidak ter-track
```
