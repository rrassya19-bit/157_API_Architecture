# 157 API Architecture

**Nama:** Ahmad Rassya Maulana  
**NIM:** 20250140157  

---

## Deskripsi
API ini menyediakan layanan RESTful untuk mengelola data komik. Dibangun menggunakan **Express.js** (versi 5) sebagai framework, **Sequelize** sebagai ORM, dan **PostgreSQL** sebagai database. API ini mendukung operasi CRUD (Create, Read, Update, Delete) untuk data komik.

---

## Prerequisites
- [Node.js](https://nodejs.org/) (v18 atau lebih baru)
- [PostgreSQL](https://www.postgresql.org/)
- [npm](https://www.npmjs.com/) (sudah termasuk dengan Node.js)
- [Postman](https://www.postman.com/) (opsional, untuk testing API)

---

## Instalasi & Menjalankan Server

### 1. Clone repositori
```bash
git clone <url-repo>
cd 157_API_Architecture
```

### 2. Inisialisasi project
```bash
npm init -y
```

### 3. Install dependencies
```bash
npm i express pg sequelize sequelize-cli dotenv nodemon
```

### 4. Inisialisasi Sequelize
```bash
npx sequelize init
```

### 5. Buat database di PostgreSQL
Buka terminal PostgreSQL atau gunakan pgAdmin, lalu buat database baru:
```sql
CREATE DATABASE nama_database;
```

### 6. Buat file `.env`
Buat file `.env` di root folder proyek, lalu isi dengan konfigurasi database Anda:

```
DB_USER=postgres
DB_PASS=password_postgres_anda
DB_DATABASE=nama_database
DB_HOST=localhost
DB_PORT=5432
DB_DIALECT=postgres
```

### 7. Jalankan server
```bash
npm start
```

Server akan berjalan di `http://localhost:3000`.  
Jika berhasil, akan muncul log:
```
Server is running on http://localhost:3000
Database connected successfully
Database synchronized
```

---

## API Endpoints

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| GET | `/api/komik` | Mengambil semua data komik |
| GET | `/api/komik/:id` | Mengambil satu komik berdasarkan ID |
| POST | `/api/komik` | Menambahkan komik baru |
| PUT | `/api/komik/:id` | Mengupdate data komik |
| DELETE | `/api/komik/:id` | Menghapus data komik |

---

## Cara Testing dengan Postman

### GET All Komik
- **Method:** GET
- **URL:** `http://localhost:3000/api/komik`
- **Response:**
```json
[
    {
        "id": 1,
        "title": "Judul Komik",
        "description": "Deskripsi komik",
        "author": "Nama Penulis",
        "createdAt": "2026-07-22T10:00:00.000Z",
        "updatedAt": "2026-07-22T10:00:00.000Z"
    }
]
```

### GET Komik by ID
- **Method:** GET
- **URL:** `http://localhost:3000/api/komik/1`
- **Response:**
```json
{
    "id": 1,
    "title": "Judul Komik",
    "description": "Deskripsi komik",
    "author": "Nama Penulis",
    "createdAt": "2026-07-22T10:00:00.000Z",
    "updatedAt": "2026-07-22T10:00:00.000Z"
}
```

### POST Tambah Komik
- **Method:** POST
- **URL:** `http://localhost:3000/api/komik`
- **Headers:** `Content-Type: application/json`
- **Body (raw JSON):**
```json
{
    "title": "One Piece",
    "description": "Petualangan bajak laut mencari harta karun",
    "author": "Eiichiro Oda"
}
```
- **Response:**
```json
{
    "id": 1,
    "title": "One Piece",
    "description": "Petualangan bajak laut mencari harta karun",
    "author": "Eiichiro Oda",
    "updatedAt": "2026-07-22T10:00:00.000Z",
    "createdAt": "2026-07-22T10:00:00.000Z"
}
```

### PUT Update Komik
- **Method:** PUT
- **URL:** `http://localhost:3000/api/komik/1`
- **Headers:** `Content-Type: application/json`
- **Body (raw JSON):**
```json
{
    "title": "Naruto",
    "description": "Petualangan ninja dari desa Konoha",
    "author": "Masashi Kishimoto"
}
```
- **Response:**
```json
{
    "id": 1,
    "title": "Naruto",
    "description": "Petualangan ninja dari desa Konoha",
    "author": "Masashi Kishimoto",
    "createdAt": "2026-07-22T10:00:00.000Z",
    "updatedAt": "2026-07-22T10:00:00.000Z"
}
```

### DELETE Hapus Komik
- **Method:** DELETE
- **URL:** `http://localhost:3000/api/komik/1`
- **Response:**
```json
{
    "message": "Komik bisa di delete"
}
```

---

## Struktur Folder

```
157_API_Architecture/
├── config/
│   ├── config.js        # Konfigurasi database dari .env
│   └── db.js            # Koneksi ke database
├── controller/
│   └── komikController.js  # Logic handler untuk setiap endpoint
├── migrations/          # File migrasi database
├── models/
│   ├── index.js         # Inisialisasi Sequelize & load model
│   └── komik.js         # Model Komik
├── routes/
│   └── api.js           # Routing semua endpoint API
├── seeders/             # Data seeder (jika ada)
├── .env                 # Environment variables (tidak di-commit)
├── .gitignore
├── index.js             # Entry point server
├── package.json
└── README.md
```

---

## Catatan Penting

- Proyek ini menggunakan **Express 5**, yang memiliki perbedaan dengan Express 4. Salah satunya: `req.body` akan bernilai `undefined` jika body kosong (tidak dikirim), bukan `{}` seperti di Express 4.
- Model database di-**sync** otomatis setiap server dijalankan (`alter: true`), jadi tidak perlu menjalankan migration secara manual.
- Pastikan file `.env` sudah diisi dengan benar sebelum menjalankan server.
- Folder `node_modules/` dan file `.env` tidak termasuk dalam Git (sudah diatur di `.gitignore`).
