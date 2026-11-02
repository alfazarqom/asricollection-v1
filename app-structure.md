# App Structure — Asri Collection

> **Dokumen:** Struktur aplikasi dan hierarki halaman frontend  
> **Versi:** 1.0  
> **Status:** Baseline struktur  
> **Repository:** `alfazarqom/asricollection-v1`  
> **Branch dokumentasi:** `docs/app-structure-v1.0`

## 1. Tujuan

Dokumen ini menetapkan struktur tingkat atas aplikasi Asri Collection, pengelompokan halaman, komponen global, serta batas tanggung jawab setiap kelompok. Dokumen ini menjadi acuan penamaan dan hierarki frontend.

Dokumen ini harus dibaca bersama:
- [list-page.md](./list-page.md) — tujuan, fitur, section, dan interaksi setiap halaman.

## 2. Struktur Utama Aplikasi

```text
App
├── AppShell
│   ├── Header
│   │   ├── AppLogo
│   │   ├── CartBtn
│   │   └── ProfileBtn
│   └── Main
│       ├── HomePage
│       ├── ProductPage
│       │   └── CategoriesPage
│       ├── SearchPage
│       ├── WishlistPage
│       ├── OrdersPage
│       └── ProfilePage
├── Standalone
│   ├── ProductDetailPage
│   ├── ProductReviewsPage
│   ├── ProductQuestionsPage
│   ├── RelatedProductsPage
│   ├── CartPage
│   ├── CheckoutPage
│   ├── AddressPage
│   ├── ShippingPage
│   ├── PaymentPage
│   ├── PaymentReturnPage
│   ├── OrderDetailPage
│   ├── OrderTrackingPage
│   └── ReturnRefundPage
├── Supporting
│   ├── NotificationsPage
│   ├── LiveChatPage
│   ├── AboutPage
│   ├── ContactPage
│   ├── FAQPage
│   ├── PoliciesPage
│   └── SystemPage
├── System
│   └── NotFoundPage
└── Overlays
    ├── Modal
    ├── BottomDrawer
    ├── QuickView
    └── Toast
```

## 3. Pengelompokan dan Tanggung Jawab

### 3.1 App

Root aplikasi yang mengatur komposisi keseluruhan frontend, penyedia state global, konfigurasi routing, dan pemanggilan layout/halaman sesuai route aktif.

### 3.2 AppShell

Kerangka utama untuk halaman-halaman utama yang menggunakan navigasi dan header aplikasi.

**Header**
- `AppLogo`: identitas dan navigasi kembali ke beranda.
- `CartBtn`: pintasan ke CartPage dan indikator jumlah item.
- `ProfileBtn`: pintasan ke ProfilePage.

**Main**
- Menjadi area render halaman utama yang sedang aktif.
- Berisi halaman Home, katalog, pencarian, Wishlist, pesanan, dan profil.
- Navigasi halaman dikelola oleh router; halaman yang tidak aktif tidak ditampilkan sebagai konten aktif.

### 3.3 Standalone

Kelompok halaman mandiri yang memiliki konteks alur atau tampilan tersendiri dan tidak menjadi anak dari area konten utama AppShell.

Halaman dalam kelompok ini:
- ProductDetailPage
- ProductReviewsPage
- ProductQuestionsPage
- RelatedProductsPage
- CartPage
- CheckoutPage
- AddressPage
- ShippingPage
- PaymentPage
- PaymentReturnPage
- OrderDetailPage
- OrderTrackingPage
- ReturnRefundPage

### 3.4 Supporting

Halaman pendukung untuk layanan pelanggan dan informasi toko:
- NotificationsPage
- LiveChatPage
- AboutPage
- ContactPage
- FAQPage
- PoliciesPage
- SystemPage

### 3.5 System

Halaman sistem untuk menangani route yang tidak ditemukan:
- NotFoundPage

### 3.6 Overlays

Komponen antarmuka kontekstual yang dapat dipanggil dari berbagai halaman. Overlay bukan halaman dan tidak menambah jumlah route halaman:
- Modal
- BottomDrawer
- QuickView
- Toast

## 4. Ringkasan Jumlah

| Kelompok | Jumlah |
|---|---:|
| AppShell | 7 |
| Standalone | 13 |
| Supporting | 7 |
| System | 1 |
| **Total halaman** | **28** |
| Overlays (komponen, bukan halaman) | 4 |

**Catatan CategoriesPage:** CategoriesPage adalah halaman/tujuan navigasi yang berada di dalam kelompok ProductPage pada hierarki yang disetujui. Untuk konsistensi inventaris, halaman ini termasuk dalam total AppShell sebanyak 7.

## 5. Prinsip Struktur

1. **Pertahankan nama dan hierarki:** nama node serta posisi pada struktur utama tidak diubah tanpa persetujuan eksplisit.
2. **Pemisahan halaman dan overlay:** Modal, BottomDrawer, QuickView, dan Toast adalah komponen overlay, bukan halaman.
3. **Satu halaman aktif:** area Main menampilkan halaman sesuai route aktif.
4. **Routing terpusat:** navigasi ant halaman dikelola melalui sistem routing aplikasi, bukan dengan menduplikasi layout di setiap halaman.
5. **Layout terpisah dari konten:** Header dan kerangka AppShell tidak ditanam ulang di setiap halaman.
6. **Mobile-first dan responsive:** struktur UI harus mendukung layar mobile sebagai prioritas dan beradaptasi pada layar yang lebih besar.
7. **Komponen dapat digunakan ulang:** komponen umum diletakkan pada lapisan bersama sesuai tanggung jawabnya, tanpa membuat duplikasi implementasi.
8. **Integrasi backend terpisah:** halaman berinteraksi dengan backend melalui service/API layer; komponen UI tidak menyimpan kredensial rahasia.
9. **Status transaksi tepercaya:** halaman pembayaran dan pesanan menampilkan status yang diberikan backend, bukan menetapkan status final dari parameter browser.
10. **Guest flow:** struktur ini tidak mengasumsikan adanya login pelanggan. Perubahan ke autentikasi pelanggan memerlukan persetujuan requirement tersendiri.

## 6. Kelompok Route

Tabel berikut menunjukkan pemetaan konseptual kelompok halaman. URL final dapat ditetapkan pada dokumen routing terpisah; pola URL di bawah bukan kontrak yang sudah dikunci.

| Kelompok | Halaman |
|---|---|
| AppShell | HomePage, ProductPage, CategoriesPage, SearchPage, WishlistPage, OrdersPage, ProfilePage |
| Standalone | ProductDetailPage, ProductReviewsPage, ProductQuestionsPage, RelatedProductsPage, CartPage, CheckoutPage, AddressPage, ShippingPage, PaymentPage, PaymentReturnPage, OrderDetailPage, OrderTrackingPage, ReturnRefundPage |
| Supporting | NotificationsPage, LiveChatPage, AboutPage, ContactPage, FAQPage, PoliciesPage, SystemPage |
| System | NotFoundPage |

## 7. Batas Tanggung Jawab

| Bagian | Tanggung jawab | Bukan tanggung jawab |
|---|---|---|
| App | Komposisi root, provider global, router | Detail UI setiap halaman |
| AppShell | Header dan kerangka halaman utama | Logika transaksi backend |
| Main | Render route halaman utama | Mengelola seluruh route aplikasi secara terpisah |
| Standalone | Menyediakan halaman untuk alur khusus | Menggandakan Header/AppShell |
| Supporting | Konten layanan dan informasi | Menentukan status transaksi |
| System | Penanganan route/error sistem | Menggantikan validasi backend |
| Overlays | Interaksi kontekstual lintas halaman | Menjadi pengganti halaman penuh |

## 8. Di Luar Cakupan

Dokumen ini tidak menetapkan:
- Struktur folder dan nama file implementasi.
- Detail route URL, route guards, atau konfigurasi React Router.
- Komponen internal setiap halaman secara lengkap.
- Skema database, tabel, kolom, atau kebijakan RLS.
- Kontrak request/response API atau Edge Function.
- Implementasi autentikasi pelanggan.
- Detail desain visual, token, dan spesifikasi responsif.
- Kebijakan harga, promosi, pengiriman, retur, atau refund yang belum ditetapkan.

Detail fitur per halaman mengacu pada `list-page.md`. Detail teknis implementasi ditetapkan dalam dokumen arsitektur atau requirement tersendiri setelah diverifikasi.

## 9. Aturan Perubahan

- Struktur ini menjadi baseline versi 1.0.
- Perubahan nama, penambahan/penghapusan halaman, atau pemindahan node harus melalui persetujuan eksplisit.
- Perubahan berikutnya dicatat sebagai versi baru; jangan menimpa baseline tanpa persetujuan.
- Setiap perubahan harus memperbarui ringkasan jumlah halaman dan referensi silang ke `list-page.md`.
