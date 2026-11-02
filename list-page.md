# List Page — Asri Collection

> **Dokumen:** Spesifikasi daftar halaman dan fitur storefront  
> **Versi:** 1.0  
> **Status:** Draft  
> **Repository:** `alfazarqom/asricollection-v1`  
> **Ruang lingkup:** Frontend pelanggan e-commerce  
> **Catatan:** Dokumen ini mendeskripsikan kebutuhan halaman dan interaksi. Detail implementasi harus mengikuti kontrak API, skema database, serta kebijakan bisnis yang telah diverifikasi.

## 1. Tujuan

Dokumen ini menjadi acuan untuk:
- Menginventarisasi seluruh halaman pelanggan.
- Menjelaskan tujuan dan fitur setiap halaman.
- Mendefinisikan section, elemen UI, dan interaksi utama.
- Menjelaskan navigasi dan keterkaitan antarhalaman.
- Mengidentifikasi fitur global dan komponen overlay.

## 2. Struktur Halaman

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

**Jumlah:** 28 halaman, 4 komponen overlay. CategoriesPage dihitung sebagai halaman tersendiri meskipun dikelompokkan di bawah ProductPage pada struktur.

## 3. AppShell — Halaman Utama

### 3.1 HomePage

**Tujuan:** Menjadi halaman beranda untuk menemukan produk dan mengakses fitur utama toko.

**Section dan elemen:**
- Header: AppLogo, CartBtn, ProfileBtn.
- Search entry: input/trigger pencarian.
- Hero: banner atau konten promosi.
- Featured products: produk unggulan.
- New arrivals: produk terbaru.
- Popular products: produk populer.
- Recommended products: rekomendasi.
- Promo information: informasi promosi yang berlaku.

**Fitur:**
- Menampilkan banner dan konten promosi.
- Menampilkan produk unggulan, terbaru, populer, dan rekomendasi.
- Membuka daftar produk dan detail produk.
- Memulai pencarian.
- Menambahkan produk ke Wishlist.
- Menambahkan produk ke Cart jika produk tersedia.
- Menampilkan indikator jumlah item Cart.

**Interaksi dan navigasi:**
- Banner atau tautan koleksi → ProductPage atau halaman tujuan yang dikonfigurasi.
- Kartu produk → ProductDetailPage.
- Ikon Wishlist → menambah/menghapus Wishlist.
- Tombol Cart → CartPage.
- Trigger pencarian → SearchPage.

### 3.2 ProductPage

**Tujuan:** Menampilkan katalog produk yang dapat dijelajahi pelanggan.

**Section dan elemen:**
- Page heading.
- Search/filter toolbar.
- Filter controls.
- Sort control.
- Product grid/list.
- Pagination atau infinite-scroll control.
- Loading, empty, dan error state.

**Fitur:**
- Menampilkan daftar produk.
- Menampilkan gambar, nama, harga, harga sebelum diskon jika tersedia, dan diskon jika tersedia.
- Menampilkan status ketersediaan dan stok secara terpisah.
- Pencarian dan filter produk.
- Sorting produk.
- Pagination atau infinite scroll.
- Menambahkan produk ke Wishlist atau Cart.
- Membuka ProductDetailPage.
- Membuka QuickView.

**Interaksi dan navigasi:**
- Kartu produk → ProductDetailPage.
- Filter kategori/koleksi → CategoriesPage atau hasil katalog terfilter.
- Search control → SearchPage.
- QuickView action → BottomDrawer/QuickView sesuai pola UI.

### 3.3 CategoriesPage

**Tujuan:** Membantu pelanggan menelusuri produk melalui kategori atau koleksi yang tersedia pada sumber data aplikasi.

**Section dan elemen:**
- Page heading.
- Category/collection list.
- Category/collection card.
- Selected category state.
- Product results.

**Fitur:**
- Menampilkan kategori atau koleksi yang memang tersedia.
- Menampilkan nama dan gambar kategori jika tersedia.
- Memilih kategori.
- Menampilkan produk berdasarkan kategori terpilih.

**Interaksi dan navigasi:**
- Memilih kategori → ProductPage dengan filter yang sesuai.
- Memilih produk → ProductDetailPage.

**Catatan data:** Jangan mengasumsikan tabel, endpoint, atau field kategori tertentu sebelum skema backend dikonfirmasi.

### 3.4 SearchPage

**Tujuan:** Menyediakan pencarian produk.

**Section dan elemen:**
- Search input.
- Search suggestions.
- Recent searches.
- Search results.
- Filter dan sort controls.
- Empty/error state.

**Fitur:**
- Mencari berdasarkan nama produk dan atribut yang didukung backend.
- Menampilkan saran pencarian jika tersedia.
- Menampilkan dan menghapus riwayat pencarian lokal jika fitur tersebut diaktifkan.
- Menampilkan hasil pencarian.
- Filter dan sorting hasil.
- Menangani hasil kosong dan kegagalan pencarian.

**Interaksi dan navigasi:**
- Submit pencarian → hasil pencarian.
- Pilih saran/riwayat → menjalankan pencarian.
- Pilih produk → ProductDetailPage.

### 3.5 WishlistPage

**Tujuan:** Menyimpan dan mengelola produk favorit pelanggan.

**Section dan elemen:**
- Page heading.
- Wishlist product list/grid.
- Product availability.
- Empty state.

**Fitur:**
- Menampilkan produk favorit.
- Menambahkan dan menghapus produk dari Wishlist.
- Memindahkan produk ke Cart.
- Menampilkan harga, ketersediaan, dan stok sesuai data.
- Menampilkan kondisi Wishlist kosong.

**Interaksi dan navigasi:**
- Pilih produk → ProductDetailPage.
- Remove → menghapus dari Wishlist.
- Add to Cart → memperbarui Cart jika produk dapat dibeli.

### 3.6 OrdersPage

**Tujuan:** Menampilkan dan mengelola riwayat pesanan pelanggan, termasuk akses pelacakan sebagai guest.

**Section dan elemen:**
- Order lookup form.
- Order list.
- Status filter.
- Order summary card.
- Empty/error state.

**Fitur:**
- Menampilkan pesanan yang dapat diakses pelanggan.
- Pencarian atau pelacakan pesanan menggunakan identitas pesanan yang diwajibkan backend.
- Filter pesanan berdasarkan status.
- Menampilkan nomor pesanan, tanggal, total, dan status.
- Membuka detail dan pelacakan pesanan.
- Menampilkan akses retur/refund jika memenuhi ketentuan.

**Interaksi dan navigasi:**
- Pilih pesanan → OrderDetailPage.
- Track order → OrderTrackingPage.
- Return/refund → ReturnRefundPage jika diizinkan.

**Catatan akses:** Jangan menampilkan seluruh pesanan publik. Backend wajib memverifikasi hak akses guest sebelum mengembalikan detail pesanan.

### 3.7 ProfilePage

**Tujuan:** Menyediakan informasi pelanggan dan pintasan ke layanan pelanggan.

**Section dan elemen:**
- Customer information.
- Account/contact details.
- Address shortcut.
- Order/Wishlist shortcut.
- Support and information links.

**Fitur:**
- Menampilkan dan mengubah data kontak yang didukung.
- Mengakses alamat.
- Mengakses pesanan dan Wishlist.
- Mengakses notifikasi dan LiveChat.
- Mengakses FAQ, Contact, dan Policies.

**Interaksi dan navigasi:**
- Address → AddressPage.
- Orders → OrdersPage.
- Wishlist → WishlistPage.
- Notifications → NotificationsPage.
- Help/support → halaman pendukung terkait.

**Catatan akses:** Jangan mengasumsikan sistem login pelanggan. Alur guest tetap menjadi baseline kecuali autentikasi pelanggan disetujui secara terpisah.

## 4. Standalone — Halaman Mandiri

### 4.1 ProductDetailPage

**Tujuan:** Menyajikan informasi lengkap dan aksi pembelian suatu produk.

**Section dan elemen:**
- Product image gallery.
- Product title and SKU.
- Price and discount information.
- Availability and stock.
- Variant selector jika produk memiliki varian.
- Quantity selector.
- Product description/details.
- Reviews summary.
- Questions summary.
- Related products.
- Purchase actions.

**Fitur:**
- Menampilkan galeri dan memperbesar gambar.
- Menampilkan nama, SKU, harga, diskon, deskripsi, stok, dan status ketersediaan.
- Memilih varian jika tersedia.
- Mengatur jumlah pembelian.
- Memvalidasi jumlah terhadap stok.
- Menambahkan ke Cart atau Wishlist.
- Memulai pembelian langsung.
- Membagikan tautan produk.
- Mengakses ulasan, pertanyaan, dan produk terkait.

**Interaksi dan navigasi:**
- Add to Cart → memperbarui Cart.
- Buy Now → Cart/Checkout sesuai aturan checkout.
- Reviews → ProductReviewsPage.
- Questions → ProductQuestionsPage.
- Related products → RelatedProductsPage.

### 4.2 ProductReviewsPage

**Tujuan:** Menampilkan ulasan pelanggan tentang produk.

**Section dan elemen:**
- Rating summary.
- Rating distribution.
- Review filters/sort.
- Review list.
- Review media.
- Empty state.

**Fitur:**
- Menampilkan rating rata-rata dan distribusi rating jika data tersedia.
- Menampilkan isi, rating, tanggal, dan media ulasan.
- Filter berdasarkan rating.
- Sorting ulasan.
- Menampilkan label pembelian terverifikasi hanya jika dapat dibuktikan backend.
- Aksi helpful jika didukung backend.

**Interaksi dan navigasi:**
- Filter/sort → memperbarui daftar ulasan.
- Kembali → ProductDetailPage.

### 4.3 ProductQuestionsPage

**Tujuan:** Menampilkan pertanyaan pelanggan dan jawaban terkait produk.

**Section dan elemen:**
- Question list.
- Answer area.
- Search/filter controls.
- Ask question form jika tersedia.
- Empty state.

**Fitur:**
- Menampilkan pertanyaan dan jawaban.
- Menampilkan tanggal dan status jawaban.
- Mencari atau mengurutkan pertanyaan.
- Mengirim pertanyaan jika mekanisme dan validasi backend tersedia.

**Interaksi dan navigasi:**
- Submit question → validasi dan pengiriman ke backend.
- Kembali → ProductDetailPage.

### 4.4 RelatedProductsPage

**Tujuan:** Menampilkan produk yang berkaitan dengan produk yang sedang dilihat.

**Section dan elemen:**
- Related products heading.
- Similar/recommended product grid.
- Empty state.

**Fitur:**
- Menampilkan produk terkait atau rekomendasi berdasarkan data yang tersedia.
- Membuka detail produk.
- Menambahkan produk ke Wishlist atau Cart.

**Interaksi dan navigasi:**
- Product card → ProductDetailPage.
- Wishlist/Cart action → memperbarui state terkait.

### 4.5 CartPage

**Tujuan:** Memeriksa dan mengelola item sebelum checkout.

**Section dan elemen:**
- Cart item list.
- Item selection.
- Quantity controls.
- Price summary.
- Availability/stock warning.
- Checkout action.
- Empty state.

**Fitur:**
- Menampilkan item Cart.
- Mengubah jumlah item.
- Memilih item untuk checkout.
- Memilih semua item.
- Menghapus item.
- Menampilkan subtotal dan jumlah item.
- Memvalidasi stok dan status ketersediaan.
- Menangani item yang tidak tersedia.
- Melanjutkan item terpilih ke CheckoutPage.

**Interaksi dan navigasi:**
- Quantity change → validasi Cart.
- Remove → menghapus item.
- Checkout → CheckoutPage.

### 4.6 CheckoutPage

**Tujuan:** Mengumpulkan dan memvalidasi informasi untuk membuat pesanan.

**Section dan elemen:**
- Customer/contact information.
- Selected items.
- Shipping address summary.
- Shipping method/fee summary.
- Order price summary.
- Place order action.
- Validation/error state.

**Fitur:**
- Menampilkan item terpilih.
- Memvalidasi data pelanggan.
- Memilih atau menambahkan alamat.
- Memilih metode pengiriman sesuai opsi yang tersedia.
- Menampilkan biaya pengiriman.
- Menampilkan subtotal dan total.
- Memvalidasi stok dan harga melalui backend.
- Membuat pesanan dan mengarahkan ke PaymentPage.

**Interaksi dan navigasi:**
- Edit address → AddressPage.
- Shipping selection → ShippingPage.
- Place order → backend membuat pesanan; hasil sukses mengarah ke PaymentPage.

**Aturan penting:** Total dari browser tidak boleh menjadi sumber kebenaran. Backend menghitung ulang harga, ongkir, stok, dan total pesanan.

### 4.7 AddressPage

**Tujuan:** Mengelola alamat pengiriman pelanggan.

**Section dan elemen:**
- Saved address list.
- Address form.
- Recipient/contact fields.
- Region and postal-code fields.
- Default address control.

**Fitur:**
- Menampilkan alamat yang dapat diakses pelanggan.
- Menambah, mengubah, dan menghapus alamat.
- Memilih alamat utama dan alamat checkout.
- Mengisi nama penerima, nomor telepon, provinsi, kota/kabupaten, kecamatan, kode pos, dan alamat lengkap.
- Menambahkan catatan alamat.

**Interaksi dan navigasi:**
- Save → validasi dan simpan.
- Select address → kembali ke konteks pemanggil dengan alamat terpilih.

### 4.8 ShippingPage

**Tujuan:** Menampilkan dan memilih opsi pengiriman.

**Section dan elemen:**
- Destination summary.
- Shipping option list.
- Delivery estimate jika tersedia.
- Shipping fee.
- Selected option state.

**Fitur:**
- Menampilkan alamat tujuan.
- Menampilkan metode/layanan pengiriman yang dikonfigurasi.
- Menampilkan estimasi jika tersedia.
- Menampilkan dan memilih biaya pengiriman.
- Mengonfirmasi pilihan.

**Interaksi dan navigasi:**
- Select shipping → menyimpan pilihan pada state checkout.
- Continue → kembali ke CheckoutPage.

**Catatan:** Jika aturan bisnis menggunakan ongkir tetap, tampilkan nilai yang dikonfigurasi backend. Jangan membuat pilihan kurir atau tarif yang tidak didukung.

### 4.9 PaymentPage

**Tujuan:** Memfasilitasi pembayaran pesanan melalui Duitku POP.

**Section dan elemen:**
- Order reference.
- Payment amount.
- Payment deadline.
- Payment instruction.
- Duitku payment action.
- Payment status.
- Error/retry state.

**Fitur:**
- Menampilkan nomor pesanan dan jumlah pembayaran.
- Menampilkan batas waktu pembayaran yang diberikan backend.
- Membuat atau mengambil invoice melalui backend.
- Membuka halaman pembayaran Duitku.
- Menampilkan status pembayaran dari backend.
- Menangani status menunggu, berhasil, gagal, atau kedaluwarsa.

**Interaksi dan navigasi:**
- Pay → meminta invoice ke backend, lalu membuka URL pembayaran yang dikembalikan.
- Refresh/check status → meminta status terkini ke backend.
- Payment return → PaymentReturnPage.

**Keamanan:** Browser redirect bukan bukti pembayaran. Status final hanya ditetapkan backend berdasarkan callback terverifikasi dan/atau rekonsiliasi yang sah. Jangan menaruh API key atau merchant secret di frontend.

### 4.10 PaymentReturnPage

**Tujuan:** Menangani pelanggan setelah kembali dari halaman pembayaran.

**Section dan elemen:**
- Payment result heading.
- Order reference.
- Verified payment status.
- Order summary.
- Next action.

**Fitur:**
- Membaca referensi pesanan dari alur return.
- Meminta status pembayaran terkini ke backend.
- Menampilkan status berhasil, menunggu, gagal, atau kedaluwarsa berdasarkan respons backend.
- Menampilkan ringkasan pesanan.
- Memberi tautan ke detail pesanan.

**Interaksi dan navigasi:**
- Verify/check → backend memeriksa status.
- Order detail → OrderDetailPage.
- Orders → OrdersPage.

### 4.11 OrderDetailPage

**Tujuan:** Menampilkan detail satu pesanan.

**Section dan elemen:**
- Order header/reference.
- Order status and payment status.
- Ordered items.
- Price breakdown.
- Shipping address/method.
- Payment information.
- Available actions.

**Fitur:**
- Menampilkan nomor dan tanggal pesanan.
- Menampilkan item, varian, jumlah, dan snapshot harga.
- Menampilkan subtotal, ongkir, dan total.
- Menampilkan alamat dan metode pengiriman.
- Menampilkan status pesanan dan pembayaran.
- Menampilkan informasi transaksi yang aman untuk pelanggan.
- Mengakses pelacakan, retur/refund, dan bantuan sesuai kelayakan.

**Interaksi dan navigasi:**
- Track → OrderTrackingPage.
- Return/refund → ReturnRefundPage jika memenuhi aturan.
- Help → LiveChatPage atau ContactPage.

### 4.12 OrderTrackingPage

**Tujuan:** Menampilkan perkembangan pemrosesan dan pengiriman pesanan.

**Section dan elemen:**
- Order reference.
- Tracking timeline.
- Current status.
- Courier and tracking number jika tersedia.
- External tracking link jika tersedia.

**Fitur:**
- Menampilkan status dan timeline.
- Menampilkan waktu perubahan status.
- Menampilkan informasi kurir dan nomor resi jika tersedia.
- Menampilkan tautan pelacakan eksternal jika disediakan.
- Menampilkan estimasi kedatangan jika tersedia.

**Interaksi dan navigasi:**
- Refresh → mengambil status terbaru dari backend.
- Order detail → OrderDetailPage.

### 4.13 ReturnRefundPage

**Tujuan:** Mengajukan dan memantau permintaan retur atau refund sesuai kebijakan toko.

**Section dan elemen:**
- Order/item selector.
- Return reason.
- Problem description.
- Evidence upload.
- Request status and history.
- Refund information.

**Fitur:**
- Menampilkan pesanan yang memenuhi syarat.
- Memilih item dan jumlah.
- Memilih alasan retur.
- Mengisi deskripsi masalah.
- Mengunggah bukti jika didukung.
- Mengirim permintaan.
- Menampilkan status, riwayat, dan keputusan.
- Menampilkan informasi refund jika tersedia.

**Interaksi dan navigasi:**
- Submit → validasi dan kirim permintaan ke backend.
- View request → menampilkan status permintaan.
- Help → LiveChatPage atau ContactPage.

## 5. Supporting — Halaman Pendukung

### 5.1 NotificationsPage

**Tujuan:** Menampilkan pemberitahuan terkait aktivitas pelanggan.

**Section dan elemen:**
- Notification list.
- Category/type indicator.
- Read/unread state.
- Empty state.

**Fitur:**
- Menampilkan notifikasi pesanan, pembayaran, pengiriman, dan promo jika tersedia.
- Menandai satu notifikasi atau seluruh notifikasi sebagai dibaca.
- Menghapus notifikasi jika didukung.
- Membuka halaman yang berkaitan dengan notifikasi.

**Interaksi:** Pilih notifikasi → navigasi ke halaman tujuan; read/delete → memperbarui status.

### 5.2 LiveChatPage

**Tujuan:** Menyediakan kanal komunikasi pelanggan dengan layanan toko.

**Section dan elemen:**
- Conversation header.
- Message history.
- Message composer.
- Attachment control jika didukung.
- Connection/service status.

**Fitur:**
- Memulai percakapan.
- Mengirim dan menerima pesan.
- Menampilkan riwayat, waktu, dan status pesan.
- Mengirim lampiran jika sistem mendukung.
- Menampilkan status layanan.

**Interaksi:** Send → validasi dan kirim; incoming message → memperbarui percakapan.

### 5.3 AboutPage

**Tujuan:** Menyampaikan informasi tentang Asri Collection.

**Section dan elemen:**
- Store introduction.
- Brand story.
- Vision and mission.
- Business information.
- Brand identity.

**Fitur:**
- Menampilkan profil, sejarah, visi/misi, dan informasi toko yang telah disetujui.

### 5.4 ContactPage

**Tujuan:** Menyediakan informasi dan formulir kontak toko.

**Section dan elemen:**
- Contact information.
- Store address and operating hours jika tersedia.
- Social links.
- Contact form.

**Fitur:**
- Menampilkan alamat, telepon, email, jam operasional, dan media sosial jika tersedia.
- Menerima pesan pelanggan melalui formulir.
- Memvalidasi dan mengirim formulir.

### 5.5 FAQPage

**Tujuan:** Menjawab pertanyaan umum pelanggan.

**Section dan elemen:**
- FAQ search.
- Topic/category grouping.
- Question and answer list.
- Empty state.

**Fitur:**
- Menampilkan FAQ berdasarkan topik.
- Mencari pertanyaan.
- Membuka/menutup jawaban.
- Mengarahkan pelanggan ke LiveChatPage atau ContactPage.

### 5.6 PoliciesPage

**Tujuan:** Menampilkan ketentuan dan kebijakan toko.

**Section dan elemen:**
- Privacy policy.
- Terms and conditions.
- Shipping policy.
- Payment policy.
- Return/refund policy.

**Fitur:**
- Menampilkan dokumen kebijakan yang berlaku.
- Menyediakan navigasi antarbagian kebijakan.
- Menampilkan versi atau tanggal pembaruan jika tersedia.

### 5.7 SystemPage

**Tujuan:** Menampilkan informasi gangguan atau kondisi sistem yang membutuhkan perhatian pelanggan.

**Section dan elemen:**
- System status/message.
- Error or maintenance explanation.
- Retry action.
- Home navigation.

**Fitur:**
- Menampilkan halaman pemeliharaan atau gangguan.
- Menampilkan pesan kesalahan yang aman.
- Menyediakan tombol coba lagi dan kembali ke HomePage.

## 6. System — Halaman Sistem

### 6.1 NotFoundPage

**Tujuan:** Menangani URL atau halaman yang tidak ditemukan.

**Section dan elemen:**
- 404 indicator.
- Explanation text.
- Navigation actions.

**Fitur:**
- Menampilkan kode dan pesan 404.
- Kembali ke HomePage.
- Kembali ke halaman sebelumnya.
- Membuka ProductPage.

## 7. Fitur Global

Fitur global digunakan lintas halaman dan bukan halaman tambahan.

| Fitur | Cakupan | Keterangan |
|---|---|---|
| Responsive layout | Semua halaman | Mobile-first dan menyesuaikan ukuran layar |
| Header navigation | AppShell | AppLogo, CartBtn, ProfileBtn |
| Cart indicator | Header dan katalog | Menampilkan jumlah item Cart |
| Search entry | HomePage/ProductPage | Mengarahkan ke SearchPage |
| Wishlist state | Katalog/detail/Wishlist | Konsistensi status favorit |
| Loading state | Halaman berbasis data | Indikator saat data dimuat |
| Empty state | Katalog, Cart, Wishlist, Orders, Search | Pesan dan aksi lanjutan |
| Error state | Semua halaman berbasis data | Pesan aman dan opsi mencoba kembali |
| Form validation | Address, Checkout, Contact, ReturnRefund | Validasi input sebelum pengiriman |
| Toast | Aksi global | Umpan balik berhasil/gagal |
| Modal | Aksi yang memerlukan konfirmasi | Misalnya konfirmasi penghapusan |
| BottomDrawer | Pilihan/detail ringkas | Interaksi kontekstual di layar kecil |
| QuickView | Katalog produk | Pratinjau produk |
| Guest order access | Orders dan tracking | Akses dibatasi oleh verifikasi backend |
| Payment status sync | Payment, Return, OrderDetail | Status bersumber dari backend |

## 8. Komponen Overlay

### 8.1 Modal
- Menampilkan konfirmasi atau informasi penting.
- Mendukung aksi konfirmasi dan pembatalan.
- Menutup melalui aksi yang jelas.
- Mengelola fokus dan aksesibilitas keyboard.

### 8.2 BottomDrawer
- Menampilkan panel dari bagian bawah layar.
- Digunakan untuk pilihan, filter, atau detail ringkas.
- Mendukung buka/tutup dan scroll konten.
- Tidak menggantikan navigasi halaman penuh untuk alur transaksi.

### 8.3 QuickView
- Menampilkan ringkasan produk dari katalog.
- Menampilkan gambar, nama, harga, ketersediaan, dan varian jika relevan.
- Menyediakan aksi detail, Wishlist, dan Cart sesuai kelayakan.

### 8.4 Toast
- Memberikan umpan balik singkat.
- Mendukung tipe informasi, sukses, peringatan, dan error.
- Tidak menjadi satu-satunya cara menyampaikan error penting.

## 9. Alur Navigasi Utama

### 9.1 Discovery dan pembelian
```text
HomePage / ProductPage / SearchPage
        ↓
ProductDetailPage
        ↓
CartPage
        ↓
CheckoutPage
        ├── AddressPage
        └── ShippingPage
        ↓
PaymentPage
        ↓
PaymentReturnPage
        ↓
OrderDetailPage
        ↓
OrderTrackingPage
```

### 9.2 Pengelolaan pelanggan
```text
ProfilePage
├── AddressPage
├── OrdersPage
│   ├── OrderDetailPage
│   └── OrderTrackingPage
├── WishlistPage
├── NotificationsPage
└── LiveChatPage
```

### 9.3 Informasi dan bantuan
```text
ProfilePage / Footer links
├── AboutPage
├── ContactPage
├── FAQPage
├── PoliciesPage
└── LiveChatPage
```

## 10. Aturan Fungsional Lintas Halaman

1. **Sumber data produk:** UI harus menggunakan sumber data backend yang ditetapkan proyek. Jangan menampilkan katalog demo sebagai fallback ketika API gagal.
2. **Ketersediaan dan stok:** Status ketersediaan untuk pembelian dan jumlah stok adalah informasi yang berbeda; tampilkan secara terpisah.
3. **Harga dan total:** Harga, ongkir, stok, dan total pesanan harus divalidasi/dihitung ulang oleh backend saat membuat pesanan.
4. **Guest checkout:** Alur pelanggan tidak boleh mengasumsikan login/register pelanggan kecuali disetujui sebagai perubahan requirement.
5. **Akses pesanan:** Nomor pesanan atau URL saja tidak boleh menjadi pengganti otorisasi. Backend harus menerapkan verifikasi akses dan membatasi data yang ditampilkan.
6. **Pembayaran:** Integrasi mengikuti dokumentasi resmi Duitku POP. API key dan merchant secret hanya berada di server. Redirect browser tidak membuktikan pembayaran berhasil.
7. **Status pembayaran:** Status final harus berasal dari backend yang memverifikasi callback dan/atau rekonsiliasi.
8. **Batas waktu pembayaran:** UI menampilkan deadline yang diberikan backend dan tidak menetapkan status kedaluwarsa sendiri.
9. **Retur/refund:** Aksi hanya tersedia jika memenuhi kebijakan dan status pesanan yang ditentukan backend.
10. **Data opsional:** Rating, review media, estimasi pengiriman, kurir, resi, rekomendasi, dan lampiran hanya ditampilkan jika sumber datanya tersedia.

## 11. Standar UI dan State

Setiap halaman yang mengambil atau mengirim data perlu mempertimbangkan state berikut:
- Initial/loading.
- Loaded/content.
- Empty.
- Validation error.
- Request/API error.
- Disabled/unavailable.
- Success feedback.
- Retry/recovery bila sesuai.

Persyaratan umum:
- Desain mobile-first dan responsive.
- Navigasi memiliki label dan fokus yang jelas.
- Form memiliki label, validasi, dan pesan error yang dapat dipahami.
- Gambar memiliki teks alternatif yang sesuai.
- Kontrol interaktif dapat digunakan dengan keyboard.
- Kontras warna dan ukuran target sentuh perlu memenuhi standar aksesibilitas yang ditetapkan design system.

## 12. Rekapitulasi

| Kelompok | Halaman | Jumlah |
|---|---|---:|
| AppShell | HomePage, ProductPage, CategoriesPage, SearchPage, WishlistPage, OrdersPage, ProfilePage | 7 |
| Standalone | ProductDetailPage, ProductReviewsPage, ProductQuestionsPage, RelatedProductsPage, CartPage, CheckoutPage, AddressPage, ShippingPage, PaymentPage, PaymentReturnPage, OrderDetailPage, OrderTrackingPage, ReturnRefundPage | 13 |
| Supporting | NotificationsPage, LiveChatPage, AboutPage, ContactPage, FAQPage, PoliciesPage, SystemPage | 7 |
| System | NotFoundPage | 1 |
| **Total** | **Seluruh halaman** | **28** |

**Overlay (bukan halaman):** Modal, BottomDrawer, QuickView, Toast — total 4 komponen.

## 13. Batas Dokumen

Dokumen ini adalah spesifikasi kebutuhan halaman tingkat awal. Dokumen ini tidak dengan sendirinya menetapkan:
- Skema tabel/database atau nama kolom.
- Bentuk payload API atau Edge Function.
- Sistem autentikasi pelanggan.
- Implementasi kategori backend.
- Tarif/kurir pengiriman di luar aturan bisnis yang telah dikonfirmasi.
- Kebijakan harga, promo, retur, dan refund yang belum ditetapkan.
- Izin untuk mengubah kode, database, konfigurasi, atau deployment.

Perubahan requirement harus ditinjau dan disetujui sebelum implementasi.
