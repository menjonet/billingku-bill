
## 📋 Deskripsi Aplikasi

**Billingku Bill** adalah sistem manajemen RTRWNet terintegrasi yang menggabungkan WhatsApp Gateway dengan portal admin web untuk mengelola layanan internet secara komprehensif. Aplikasi ini dirancang khusus untuk RTRWNet yang membutuhkan solusi all-in-one untuk manajemen pelanggan, billing, monitoring, dan notifikasi.

### 🎯 Fitur Utama

- **🔧 WhatsApp Bot Gateway** - Interface perintah via WhatsApp dengan role-based access control
- **🌐 Web Portal Admin** - Dashboard admin yang lengkap dengan versioning system
- **💳 Sistem Billing Terintegrasi** - Manajemen tagihan dan pembayaran
- **💳 Payment Gateway** - Integrasi Midtrans, Xendit, Tripay
- **📊 GenieACS Management** - Monitoring dan manajemen perangkat ONU/ONT
- **🛠️ Mikrotik Management** - Manajemen PPPoE dan Hotspot
- **📱 Portal Pelanggan** - Self-service untuk pelanggan
- **📈 Monitoring Real-time** - PPPoE, RX Power, dan sistem dengan grafik terpisah
- **🔔 Notifikasi Otomatis** - WhatsApp notifications
- **📋 Trouble Ticket System** - Manajemen gangguan via WhatsApp dan web
- **👥 Role-Based Access Control** - Super Admin, Admin, Technician, Customer
- **📱 WhatsApp Commands** - Trouble report, PPPoE management, version info
- **🎨 Enhanced UI** - Traffic graphs separation, high bandwidth support, admin settings cleanup

---

## 📱 WhatsApp Commands

### 👑 **Admin Commands** *(Super Admin & Admin)*
- **`admin`** - Menu bantuan khusus admin
- **`cekstatus [nomor]`** - Cek status pelanggan berdasarkan nomor
- **`gantissid [nomor] [ssid_baru]`** - Ganti SSID WiFi pelanggan
- **`reboot [nomor]`** - Reboot perangkat pelanggan
- **`status`** - Cek status sistem dan koneksi
- **`restart`** - Restart layanan WhatsApp
- **`version`** - Tampilkan informasi versi aplikasi
- **`info`** - Tampilkan informasi sistem lengkap

### 🔧 **Technician Commands** *(Admin & Technician)*
- **`teknisi`** - Menu bantuan khusus teknisi
- **`trouble`** - Lihat daftar laporan gangguan
- **`status [id]`** - Cek status laporan gangguan tertentu
- **`update [id] [status] [catatan]`** - Update status laporan
- **`selesai [id] [catatan]`** - Tandai laporan selesai
- **`addpppoe [user] [pass] [profile] [ip] [info]`** - Tambah user PPPoE
- **`editpppoe [user] [field] [value]`** - Edit field user PPPoE
- **`delpppoe [user] [alasan]`** - Hapus user PPPoE
- **`pppoe [filter]`** - List semua user PPPoE
- **`checkpppoe [user]`** - Cek status user PPPoE
- **`restartpppoe [user]`** - Restart koneksi user PPPoE

### 👤 **Customer Commands** *(Semua User)*
- **`menu`** - Menu umum untuk semua user
- **`billing`** - Menu bantuan untuk fitur billing
- **`cekstatus [nomor]`** - Cek status pelanggan (terbatas)
- **`version`** - Tampilkan informasi versi aplikasi

### 📚 **Help Commands**
- **`help trouble`** - Bantuan untuk fitur trouble report
- **`help pppoe`** - Bantuan untuk fitur PPPoE management

---

## 🚀 Instalasi

### Persyaratan Sistem

- **Node.js** v18+ (direkomendasikan v20+)
- **npm** atau yarn
- **GenieACS** API access
- **Mikrotik** API access
- **WhatsApp** number untuk bot
- **Database SQLite** (built-in)

### 1. Clone Repository

```bash
# Install git jika belum ada
apt install git curl -y

# Clone repository
git clone https://github.com/menjonet/mj-bill
cd mj-bill
```

### 2. Install Dependencies

```bash
# Install semua dependencies
npm install
```

### 3. Konfigurasi Settings


### 4. Setup Database

```bash
# Jalankan script untuk setup database billing
node scripts/add-payment-gateway-tables.js
```

### 5. Menjalankan Aplikasi

**Development Mode:**
```bash
npm run dev
```

**Production Mode:**
```bash
npm start
```

**Dengan PM2:**
```bash
# Install PM2 jika belum ada
npm install -g pm2

# Start aplikasi
pm2 start app.js --name billingku-bill

# Monitor aplikasi
pm2 monit

# View logs
pm2 logs billingku-bill
```

### 6. Setup WhatsApp Bot

1. **Siapkan 2 nomor WhatsApp:**
   - 1 nomor untuk bot (akan scan QR code)
   - 1 nomor untuk admin (untuk mengirim perintah)

2. **Scan QR Code** yang muncul di terminal untuk login WhatsApp bot

3. **Test dengan perintah**: `status` atau `menu`

---

## 🌐 Akses Web Portal

- **Portal Pelanggan**: `http://ipserver:3003`
- **Admin Dashboard**: `http://ipserver:3003/admin/login`
- **Login Admin**: Username dan password yang dikonfigurasi di `settings.json`

---

## 💳 Sistem Billing

### Fitur Billing

- **📊 Dashboard Billing** - Statistik real-time
- **👥 Manajemen Pelanggan** - CRUD pelanggan dengan PPPoE username
- **📦 Manajemen Paket** - Paket internet dengan harga
- **📄 Manajemen Invoice** - Buat, edit, hapus tagihan
- **💰 Manajemen Pembayaran** - Tracking pembayaran
- **🔄 Auto Invoice** - Generate tagihan otomatis
- **💳 Payment Gateway** - Integrasi Midtrans, Xendit, Tripay
- **📱 WhatsApp Notifications** - Notifikasi tagihan dan pembayaran

### Payment Gateway

Aplikasi mendukung 3 payment gateway populer di Indonesia:

1. **Midtrans** - Payment gateway terpopuler
2. **Xendit** - Payment gateway enterprise
3. **Tripay** - Payment gateway lokal

**Setup Payment Gateway:**
1. Akses `/admin/billing/payment-settings`
2. Pilih gateway yang aktif
3. Masukkan API keys
4. Test koneksi
5. Aktifkan production mode

---

## 🔧 WhatsApp Bot Commands

### Perintah untuk Pelanggan
- `menu` - Menampilkan menu bantuan
- `status` - Cek status perangkat
- `refresh` - Refresh data perangkat
- `gantiwifi [nama]` - Ganti nama WiFi
- `gantipass [password]` - Ganti password WiFi
- `info` - Informasi layanan
- `speedtest` - Test kecepatan internet

### Perintah untuk Admin

#### GenieACS Commands
- `devices` - Daftar perangkat
- `cekall` - Cek semua perangkat
- `cek [nomor]` - Cek status ONU
- `cekstatus [nomor]` - Cek status pelanggan
- `admincheck [nomor]` - Cek perangkat admin
- `gantissid [nomor] [ssid]` - Ubah SSID
- `gantipass [nomor] [pass]` - Ubah password
- `reboot [nomor]` - Restart ONU
- `factory reset [nomor]` - Reset factory
- `refresh` - Refresh data perangkat
- `tag [nomor] [tag]` - Tambah tag pelanggan
- `untag [nomor] [tag]` - Hapus tag
- `tags [nomor]` - Lihat tags
- `addtag [device_id] [nomor]` - Tambah tag perangkat
- `addppoe_tag [pppoe_id] [nomor]` - Tambah tag dengan id pppoe
- `adminssid [nomor] [ssid]` - Admin ubah SSID
- `adminrestart [nomor]` - Admin restart ONU
- `adminfactory [nomor]` - Admin factory reset
- `confirm admin factory reset [nomor]` - Konfirmasi factory reset

#### Mikrotik Commands
- `interfaces` - Daftar interface
- `interface [nama]` - Detail interface
- `enableif [nama]` - Aktifkan interface
- `disableif [nama]` - Nonaktifkan interface
- `ipaddress` - Alamat IP
- `routes` - Tabel routing
- `dhcp` - DHCP leases
- `ping [ip] [count]` - Test ping
- `logs [topics] [count]` - Log Mikrotik
- `firewall [chain]` - Status firewall
- `users` - Daftar semua user
- `profiles [type]` - Daftar profile
- `identity [nama]` - Info router
- `clock` - Waktu router
- `resource` - Info resource
- `reboot` - Restart router
- `confirm restart` - Konfirmasi restart

#### Hotspot & PPPoE Management
- `vcr [user] [profile] [nomor]` - Buat voucher
- `hotspot` - User hotspot aktif
- `pppoe` - User PPPoE aktif
- `offline` - User PPPoE offline
- `addhotspot [user] [pass] [profile]` - Tambah user
- `addpppoe [user] [pass] [profile] [ip]` - Tambah PPPoE
- `setprofile [user] [profile]` - Ubah profile
- `delhotspot [username]` - Hapus user hotspot
- `delpppoe [username]` - Hapus user PPPoE
- `addpppoe_tag [user] [nomor]` - Tambah tag PPPoE
- `member [username] [profile] [nomor]` - Tambah member
- `list` - Daftar semua user
- `remove [username]` - Hapus user (generic)
- `addadmin [nomor]` - Tambah nomor admin
- `removeadmin [nomor]` - Hapus nomor admin

#### Sistem & Admin
- `otp [nomor]` - Kirim OTP
- `status` - Status sistem
- `logs` - Log aplikasi
- `restart` - Restart aplikasi
- `debug resource` - Debug resource
- `checkgroup` - Cek status group
- `setadmin [nomor]` - Set nomor admin
- `settechnician [nomor]` - Set nomor teknisi
- `setheader [teks]` - Set header pesan
- `setfooter [teks]` - Set footer pesan
- `setgenieacs [url] [user] [pass]` - Set GenieACS
- `setmikrotik [host] [port] [user] [pass]` - Set Mikrotik
- `admin` - Menu admin
- `help` - Bantuan perintah
- `ya/iya/yes` - Konfirmasi ya
- `tidak/no/batal` - Konfirmasi tidak
- `addwan [interface]` - Tambah WAN

#### WiFi & Layanan
- `info wifi` - Info WiFi pelanggan
- `info` - Info layanan
- `gantiwifi [ssid]` - Ganti nama WiFi
- `gantipass [password]` - Ganti password WiFi
- `speedtest` - Test kecepatan
- `diagnostic` - Diagnostik perangkat
- `history` - Riwayat perangkat
- `menu` - Menu utama
- `factory reset` - Reset factory (pelanggan)
- `confirm factory reset` - Konfirmasi factory reset


