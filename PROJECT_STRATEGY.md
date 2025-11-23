# Architecture & Design Document

Dokumen ini menjelaskan keputusan arsitektur, pola desain, dan strategi teknis yang digunakan dalam pengembangan aplikasi Fullstack CRM/ERP ini.

## 1. High-Level Architecture

Sistem ini menggunakan arsitektur **Client-Server** yang terpisah (Decoupled) namun dikelola dalam satu repository (**Monorepo**).

```mermaid
graph TD
    User[User Browser] -->|HTTP/HTTPS| NextJS[Frontend (Next.js)]
    NextJS -->|REST API (JSON)| NestJS[Backend (NestJS)]
    NestJS -->|TypeORM| DB[(PostgreSQL)]
```

### Komponen

1.  **Frontend (Consumer)**: Bertanggung jawab atas presentasi, interaksi user, dan rendering halaman (SSR/CSR).
2.  **Backend (Provider)**: Bertanggung jawab atas logika bisnis, validasi data, keamanan, dan persistensi data.
3.  **Database**: Penyimpanan data relasional yang persisten.

## 2. Monorepo Strategy (Turborepo)

Kami memilih pendekatan Monorepo menggunakan **Turborepo** dengan alasan:

- **Unified Workflow**: Satu perintah untuk menjalankan seluruh stack (`npm run dev`).
- **Shared Configuration**: ESLint, Prettier, dan TypeScript config bisa dibagi antar project.
- **Type Safety (Future)**: Memungkinkan sharing DTO (Data Transfer Objects) antara Backend dan Frontend tanpa duplikasi kode.

## 3. Backend Design (NestJS)

Backend dibangun dengan prinsip **Modular Architecture**.

### Pola Desain

- **Controller**: Menangani request HTTP dan response.
- **Service**: Berisi logika bisnis utama.
- **Repository/TypeORM**: Menangani query ke database.
- **DTO (Data Transfer Object)**: Mendefinisikan bentuk data yang dikirim antar layer.

### Security

- **Authentication**: Menggunakan **JWT (JSON Web Token)**. Stateless authentication yang scalable.
- **Authorization**: Role-based access control (RBAC) menggunakan Guards.
- **Encryption**: Password di-hash menggunakan `bcrypt` sebelum disimpan.

## 4. Frontend Design (Next.js)

Frontend menggunakan **App Router** terbaru dari Next.js.

### Data Fetching Strategy

1.  **Server Components**: Fetch data sensitif atau data awal langsung di server (Node.js environment) untuk performa dan SEO.
2.  **Client Components**: Fetch data interaktif menggunakan `useEffect` atau library seperti `SWR`/`TanStack Query`.

### Authentication Flow

1.  User login di form Frontend.
2.  Frontend kirim credential ke Backend.
3.  Backend validasi -> kirim `access_token`.
4.  Frontend menyimpan token (rekomendasi: HTTP-Only Cookie atau Secure Storage) dan menyertakannya di setiap request berikutnya (Authorization Header).

## 5. Scalability & Performance

- **Backend**: Stateless, sehingga bisa di-scale horizontal (menambah instance server) dengan mudah di balik Load Balancer.
- **Frontend**: Halaman statis di-cache oleh CDN (jika deploy di Vercel), halaman dinamis di-render di server (SSR).
- **Database**: Menggunakan PostgreSQL yang terbukti tangguh untuk data relasional kompleks.
