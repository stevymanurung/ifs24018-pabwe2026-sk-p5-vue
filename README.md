# Delcom Auction — ifs24018-pabwe2026-sk-p5-vue

Aplikasi lelang online (Praktikum PABWE 2026, Studi Kasus 1) berbasis **Vue 3 + JavaScript**, **Pinia**, **Vue Router**, **Tailwind CSS v4**, **SweetAlert2**, dan **@toast-ui/editor**. Data berasal dari https://open-api.delcom.org/docs/1.0/api-aucations.

## Menjalankan
```bash
bun install          # atau: npm install
cp .env.example .env # isi VITE_DELCOM_BASEURL dan APP_PORT
bun run dev          # http://localhost:3000
bun run build        # build produksi (dist/)
bun run test:coverage # Vitest + coverage v8 (threshold 100%)
```

## Rute
| Path | Halaman | Akses |
|---|---|---|
| `/auth/login` | Login | publik |
| `/auth/register` | Registrasi | publik |
| `/` | Dashboard lelang (filter, pencarian) | login |
| `/aucations/:aucationId` | Detail lelang + riwayat bid | login |
| `/users` | Daftar pengguna | login |
| `/profile` | Profil & pengaturan akun | login |
| `/:pathMatch(.*)*` | 404 | publik |

Login memakai selector `#login-email-input`, `#login-password-input`, `#login-submit-button`.

## Deploy (Vercel/Netlify)
`vercel.json` dan `public/_redirects` sudah disertakan agar rute SPA tidak 404 saat refresh. Set env `VITE_DELCOM_BASEURL`.

## Catatan implementasi
- Endpoint ganti kata sandi memakai `PUT /users/password` sesuai dokumentasi API resmi.
- Tab "Berlangsung"/"Ditutup" difilter di sisi klien berdasarkan `closed_at` agar akurat; "Lelang Saya" memakai `is_me=1`.
- `ModalShell.vue` adalah komponen pembungkus dialog (fokus, Escape, aria) yang dipakai keempat modal.
