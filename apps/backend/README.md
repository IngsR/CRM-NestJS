# Backend API (NestJS)

Aplikasi backend ini dibangun menggunakan **NestJS**, sebuah framework Node.js yang efisien dan scalable untuk membangun aplikasi server-side. Backend ini berfungsi sebagai **REST API** yang menyediakan data untuk Frontend (Next.js).

## ✨ Fitur Utama

- **RESTful API**: Mengikuti standar REST untuk komunikasi data.
- **Database ORM**: Menggunakan **TypeORM** untuk interaksi aman dengan PostgreSQL.
- **Authentication**: Implementasi **JWT (JSON Web Token)** untuk keamanan endpoint.
- **Validation**: Validasi input otomatis menggunakan `class-validator` dan DTO.
- **Swagger UI**: Dokumentasi API interaktif yang tergenerate otomatis.

## 🚀 Menjalankan Backend Saja

Jika Anda hanya ingin menjalankan backend tanpa frontend:

```bash
# Dari root folder
npm run dev --filter=@repo/backend
```

Atau masuk ke direktori backend:

```bash
cd apps/backend
npm run start:dev
```

Akses API di: `http://localhost:3000`

## 📚 Dokumentasi API (Swagger)

Kami menggunakan Swagger untuk mendokumentasikan endpoint API secara otomatis.
Setelah server berjalan, buka browser dan akses:

👉 **[http://localhost:3000/api](http://localhost:3000/api)**

Di sini Anda bisa melihat daftar endpoint, format request/response, dan mencoba API langsung (Try it out).

## 🔧 Konfigurasi Environment (.env)

Pastikan Anda memiliki file `.env` di dalam folder `apps/backend` dengan konfigurasi berikut:

```env
# Database Config
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=password_anda
DB_DATABASE=nama_database

# JWT Secret
JWT_SECRET=rahasia_super_aman
JWT_EXPIRATION_TIME=3600
```

## 🧪 Testing

Backend ini dilengkapi dengan unit test dan e2e test.

```bash
# Menjalankan Unit Tests
npm run test

# Menjalankan E2E Tests
npm run test:e2e
```
