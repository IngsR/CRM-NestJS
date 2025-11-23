# Frontend UI (Next.js)

Aplikasi frontend ini dibangun menggunakan **Next.js 15** (App Router), framework React paling populer untuk membangun aplikasi web modern yang cepat dan SEO-friendly. Frontend ini bertugas menampilkan antarmuka pengguna dan berinteraksi dengan Backend API.

## ✨ Fitur Utama

- **App Router**: Menggunakan routing terbaru Next.js yang berbasis file system.
- **Server Components**: Fetching data dilakukan di server untuk performa maksimal.
- **Tailwind CSS**: Styling utility-first untuk desain yang cepat dan responsif.
- **TypeScript**: Type-safety untuk mencegah bug saat pengembangan.

## 🚀 Menjalankan Frontend Saja

Jika Anda hanya ingin menjalankan frontend (pastikan backend juga berjalan agar data tampil):

```bash
# Dari root folder
npm run dev --filter=@repo/frontend
```

Atau masuk ke direktori frontend:

```bash
cd apps/frontend
npm run dev
```

Akses UI di: `http://localhost:3001` (atau port yang tersedia).

## 🔧 Konfigurasi Environment (.env.local)

Buat file `.env.local` di dalam folder `apps/frontend` untuk menyimpan konfigurasi environment frontend:

```env
# URL Backend API
NEXT_PUBLIC_API_URL=http://localhost:3000
```

## 📂 Struktur Folder Penting

- `app/`: Berisi halaman-halaman aplikasi (Routes).
- `components/`: Komponen UI yang dapat digunakan kembali (Button, Card, Navbar).
- `lib/`: Utility functions dan konfigurasi API client.
- `public/`: Aset statis seperti gambar dan font.

## 📦 Integrasi dengan Backend

Frontend ini berkomunikasi dengan Backend NestJS melalui REST API.
Kami menyarankan penggunaan pola **Service/Repository** di frontend atau library seperti `TanStack Query` untuk manajemen state server yang lebih kompleks di masa depan.
