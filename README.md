# 🛡️ Automated Recon & Subdomain Discovery Tool

**Author:** Bela Agustina

**Project Category:** Cyber Security – Information Gathering Automation

**Repository:** `recon-automation-bella`

---

## 📝 1. Project Title & Description

**Recon-Automation** adalah tool otomasi berbasis Bash untuk mempercepat fase **Reconnaissance** pada pengujian keamanan web. Tool ini mengintegrasikan beberapa OSINT tools populer untuk menemukan subdomain dan memvalidasi host aktif secara massal dengan sistem logging dan reporting terstruktur.

### 🎯 Tujuan Utama

Meningkatkan efisiensi waktu dalam proses pengumpulan aset domain selama tahap information gathering.

### ⭐ Fitur Unggulan

* Instalasi tools otomatis
* Enumerasi subdomain terintegrasi
* Deduplikasi menggunakan **anew**
* Validasi host aktif menggunakan **httpx**
* Logging & error handling
* Struktur folder hasil scan otomatis
* Laporan statistik per domain dan global
  

## 2. Struktur Directory

```
recon-automation-belaagustina/
│
├── input/                       # Data awal sebelum scanning
│   └── domains.txt              # Daftar domain target
│
├── scripts/                     # Tempat script utama
│   └── recon-auto.sh            # Script automation recon
│
├── output/                      # Semua hasil scan tersimpan di sini
│   └── recon_<timestamp>/       # Folder hasil berdasarkan waktu scan
│       │
│       ├── all-subdomains.txt   # Gabungan semua subdomain unik
│       ├── all-live.txt         # Gabungan semua host aktif
│       ├── domain-summary.txt   # Statistik jumlah subdomain per domain
│       │
│       ├── example.com/         # Hasil khusus domain example.com
│       │   ├── subs.txt         # Subdomain domain tersebut
│       │   └── live.txt         # Host aktif domain tersebut
│       │
│       ├── tesla.com/           # Hasil khusus domain tesla.com
│       │   ├── subs.txt
│       │   └── live.txt
│       │
│       └── logs/                # Catatan proses
│           ├── progress.log     # Log aktivitas script
│           └── errors.log       # Log error jika ada masalah
│
└── README.md                    # Dokumentasi project


```

### 📌 Penjelasan Struktur

| Folder/File               | Fungsi                                            |
| ------------------------- | ------------------------------------------------- |
| **subs.txt (per domain)** | Hasil enumerasi subdomain khusus domain tersebut  |
| **live.txt (per domain)** | Host aktif dari domain tersebut                   |
| **all-subdomains.txt**    | Gabungan semua subdomain unik dari seluruh target |
| **all-live.txt**          | Gabungan semua live hosts                         |
| **domain-summary.txt**    | Tabel statistik per domain                        |
| **logs/**                 | Log aktivitas dan error selama scanning           |

Struktur ini memisahkan hasil **per target** sekaligus menyediakan **rekap global**, seperti workflow profesional di environment SOC/pentest.

---

## 🛠️ 3. Environment Setup

Tool ini dirancang dengan konsep **Run and Go**.

### Prasyarat

* OS berbasis Debian/Kali Linux
* Koneksi internet aktif

### Install PDTM (disarankan)

```bash
curl -fsSL https://get.pdtm.sh | bash
pdtm -install subfinder httpx
```

### Install Golang

```bash
sudo apt update
sudo apt install golang-go -y
```

### Install Anew

```bash
go install github.com/tomnomnom/anew@latest
export PATH=$PATH:$(go env GOPATH)/bin
```

> Script juga mampu mendeteksi dan menginstal tools otomatis jika belum tersedia.

---

## 🚀 4. Cara Menjalankan Script

```bash
cd ~/recon-automation-belaagustina
chmod +x scripts/recon-auto.sh
./scripts/recon-auto.sh
```

Script akan membuka terminal baru dan menjalankan proses scanning otomatis.

---

## 📂 5. Contoh Input & Output

### Input (`input/domains.txt`)

```
google.com
tesla.com
example.com
target.id
sample.net
```

### Output yang Dihasilkan

| File               | Fungsi                   |
| ------------------ | ------------------------ |
| all-subdomains.txt | Semua subdomain unik     |
| all-live.txt       | Host aktif + status code |
| domain-summary.txt | Statistik per domain     |
| progress.log       | Log proses               |
| errors.log         | Log error                |

---

## 🔍 6. Penjelasan Bagian Kode

| Modul                      | Fungsi                                                                                                       |
| -------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Module Check & Install** | Mengecek tools via `command -v`. Jika tidak ada, script menjalankan `go install` dan mengatur PATH otomatis. |
| **Environment Fix**        | `unset GOROOT` untuk mencegah konflik instalasi Go lama.                                                     |
| **Execution Engine**       | Menggunakan `gnome-terminal` agar proses berjalan di jendela baru.                                           |
| **Enumeration Engine**     | `subfinder` mencari subdomain secara pasif.                                                                  |
| **Data Filtering**         | `anew` mencegah duplikasi subdomain.                                                                         |
| **Live Host Detection**    | `httpx` mengecek host aktif beserta status HTTP dan title.                                                   |
| **Logging System**         | Semua proses dicatat dengan timestamp via `tee`.                                                             |
| **Error Handling**         | stderr diarahkan ke `logs/errors.log`.                                                                       |
| **Reporting Engine**       | `awk`, `wc -l`, dan `printf` menghasilkan tabel statistik rapi.                                              |

---

## 📊 7. Final Output Metrics

Script menampilkan:

* Total domain diproses
* Total subdomain unik
* Total live hosts aktif
* Durasi scan

---

## 🖥 8. Screenshots

Tambahkan screenshot berikut:

**Figure 1. Recon automation execution**

```
![Execution](screenshots/execution.png)
```

**Figure 2. Live hosts discovered**

```
![Live Hosts](screenshots/live-hosts.png)
```

**Figure 3. Output directory structure**

```
![Directory](screenshots/tree.png)
```

---

## 🧩 9. Key Highlights

✔ End-to-end recon automation
✔ Logging & error handling
✔ Deduplication system
✔ Structured reporting
✔ SOC-style workflow simulation

---

## 👤 Author

**Bela Agustina**
Cyber Security Student

---

> This project simulates a real-world reconnaissance automation pipeline aligned with penetration testing and SOC operational workflows.
