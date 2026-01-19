---
layout: ../../layouts/DocsLayout.astro
title: Panduan Pengguna & Dokumentasi
---

<p class="text-lg text-slate-300 mb-12 leading-relaxed">
Selamat datang di dokumentasi resmi <strong class="text-white">Deep Learning Land Cover Toolbox v2.1.0</strong>. 
Panduan ini akan menuntun Anda langkah demi langkah mulai dari instalasi hingga melakukan klasifikasi tutupan lahan menggunakan Citra Landsat 8 dan Kecerdasan Buatan (AI) di ArcGIS Pro.
</p>

<h2 id="persiapan-awal" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">📦 Persiapan Awal (Instalasi)</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400 mb-4">
Sebelum memulai, pastikan Anda telah mengunduh file toolbox. Ikuti langkah berikut untuk memasukkannya ke dalam ArcGIS Pro:
</p>
<ol class="space-y-3 text-slate-300 list-decimal list-inside marker:text-emerald-500 marker:font-bold">
<li class="pl-2"><strong class="text-white">Ekstrak</strong> file ZIP yang telah diunduh ke folder yang aman (contoh: <code>D:\GIS_Tools\</code>).</li>
<li class="pl-2">Buka aplikasi <strong class="text-white">ArcGIS Pro</strong>.</li>
<li class="pl-2">Buka panel <strong class="text-white">Catalog Pane</strong> (biasanya di sebelah kanan).</li>
<li class="pl-2">Klik kanan pada <strong class="text-white">Toolboxes</strong> > pilih <strong class="text-emerald-400">Add Toolbox</strong>.</li>
<li class="pl-2">Cari dan pilih file <code>DeepLearningLandCover.pyt</code>.</li>
</ol>
</div>

<div class="my-8 rounded-2xl overflow-hidden border border-white/10 shadow-2xl">
<img src="/screenshots/tool-list.png" alt="Struktur Toolbox di ArcGIS Pro" class="w-full h-auto object-cover" />
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="step-1-libs" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🛠️ Langkah 1: Instalasi Library (Smart Installer)</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400 mb-4">
Setelah toolbox ditambahkan, Anda wajib menginstal library Deep Learning (<em>PyTorch</em> & <em>FastAI</em>). Versi 2.1.0 kini dilengkapi dengan <strong>Smart Installer</strong> yang secara otomatis mendeteksi hardware Anda.
</p>
<ol class="space-y-3 text-slate-300 list-decimal list-inside marker:text-emerald-500 marker:font-bold">
<li class="pl-2">Buka tool <strong class="text-white">"01. Install Deep Learning Libraries (Otomatis)"</strong>.</li>
<li class="pl-2">Centang <strong class="text-emerald-400">"Gunakan GPU (CUDA)"</strong> jika Anda memiliki kartu grafis NVIDIA.</li>
<li class="pl-2">Klik <strong>Run</strong> dan perhatikan jendela <em>Messages</em> untuk hasil deteksi hardware.</li>
</ol>
</div>

<div class="grid md:grid-cols-2 gap-8 my-12">
<div class="bg-slate-900/50 border border-white/10 rounded-2xl p-6 shadow-xl">
<h4 class="text-emerald-400 font-bold mb-4 flex items-center gap-2">
<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M11 3a1 1 0 10-2 0v1a1 1 0 102 0V3zM15.657 5.757a1 1 0 00-1.414-1.414l-.707.707a1 1 0 001.414 1.414l.707-.707zM18 10a1 1 0 01-1 1h-1a1 1 0 110-2h1a1 1 0 011 1zM5.05 6.464A1 1 0 106.464 5.05l-.707-.707a1 1 0 00-1.414 1.414l.707.707zM5 10a1 1 0 01-1 1H3a1 1 0 110-2h1a1 1 0 011 1zM8 16v-1a1 1 0 112 0v1a1 1 0 11-2 0zM13.536 14.95a1 1 0 011.414 0l.707.707a1 1 0 01-1.414 1.414l-.707-.707a1 1 0 010-1.414zM16.121 17.243a1 1 0 011.414 0l.707.707a1 1 0 01-1.414 1.414l-.707-.707a1 1 0 010-1.414z" /></svg>
Akselerasi GPU (Recommended)
</h4>
<p class="text-sm text-slate-400 mb-4 leading-relaxed">
Sistem akan mengecek apakah GPU NVIDIA Anda siap digunakan. Jika CUDA Toolkit belum terinstal, sistem akan menawarkan <strong>Download Otomatis (~3GB)</strong>.
</p>
<ul class="text-xs text-slate-500 space-y-2">
<li>✅ 10x Lebih cepat dibanding CPU.</li>
<li>✅ Otomatis mendeteksi Driver NVIDIA.</li>
<li>✅ Memasang bundle PyTorch GPU (cu118).</li>
</ul>
</div>
<div class="bg-slate-900/50 border border-white/10 rounded-2xl p-6 shadow-xl">
<h4 class="text-blue-400 font-bold mb-4 flex items-center gap-2">
<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" /></svg>
Mode CPU (Universal)
</h4>
<p class="text-sm text-slate-400 mb-4 leading-relaxed">
Jika laptop Anda tidak memiliki GPU NVIDIA, sistem akan memasang versi CPU yang <strong>dijamin berhasil</strong> di semua perangkat.
</p>
<ul class="text-xs text-slate-500 space-y-2">
<li>✅ Kompatibel dengan semua processor.</li>
<li>✅ Tanpa perlu konfigurasi tambahan.</li>
<li>⚠️ Proses klasifikasi akan lebih lambat.</li>
</ul>
</div>
</div>

<div class="mb-12 p-6 bg-amber-500/10 border border-amber-500/20 rounded-2xl">
<h4 class="text-amber-400 font-bold mb-3 flex items-center gap-2">
<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" /></svg>
Penting: Restart ArcGIS Pro
</h4>
<p class="text-sm text-slate-300 leading-relaxed">
Sistem akan menampilkan dialog konfirmasi setelah instalasi selesai. Klik <strong class="text-white">Yes</strong> untuk melakukan restart otomatis agar perubahan library dapat diterapkan sepenuhnya oleh ArcGIS Pro.
</p>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="manual-cuda" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">📀 Panduan Instalasi CUDA Manual (Opsional)</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400 mb-6">
Jika Smart Installer gagal mengunduh otomatis atau Anda ingin melakukan instalasi secara mandiri, ikuti panduan berikut untuk mengaktifkan akselerasi GPU secara manual.
</p>

<div class="space-y-8">
<div>
<h4 class="text-white font-bold mb-3 flex items-center gap-2">
1. Unduh CUDA Toolkit 11.8
</h4>
<p class="text-sm text-slate-400 mb-4">
Deep Learning di ArcGIS Pro versi ini dioptimalkan untuk <strong>CUDA 11.8</strong>. Versi lain mungkin menyebabkan konflik library.
</p>
<a href="https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exe_local" target="_blank" class="inline-flex items-center gap-2 text-emerald-400 hover:text-emerald-300 font-medium transition-colors">
Download CUDA 11.8 dari NVIDIA Official Site →
</a>
</div>

<div class="border-l-2 border-white/10 pl-6">
<h4 class="text-white font-bold mb-3">2. Langkah Instalasi</h4>
<ul class="space-y-3 text-sm text-slate-400 list-disc list-inside">
<li>Jalankan installer <code>cuda_11.8.0_522.06_windows.exe</code>.</li>
<li>Pilih opsi <strong class="text-white">Custom (Advanced)</strong>.</li>
<li>Pastikan <strong class="text-emerald-400">CUDA</strong> tercentang. Anda boleh menghilangkan centang pada <em>Display Driver</em> jika driver Anda sudah versi terbaru.</li>
<li>Tunggu hingga selesai dan <strong>Restart Komputer</strong>.</li>
</ul>
</div>

<div class="p-4 bg-emerald-500/5 border border-emerald-500/20 rounded-xl">
<h4 class="text-emerald-400 font-bold mb-2">3. Verifikasi di ArcGIS Pro</h4>
<p class="text-xs text-slate-400 leading-relaxed">
Setelah instalasi manual selesai, jalankan kembali tool <strong>01. Install Deep Learning Libraries</strong> dengan opsi <strong class="text-white">"Gunakan GPU (CUDA)"</strong> tercentang. Tool akan mendeteksi CUDA yang baru Anda instal dan mengonfigurasi PyTorch secara otomatis.
</p>
</div>
</div>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="step-2-manage" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🛰️ Langkah 2: Persiapan Data (Manage Landsat 8)</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400">
Toolbox ini membutuhkan input berupa <strong>Mosaic Dataset</strong> atau <strong>Raster Dataset</strong>. Gunakan tool ini untuk merapikan data mentah Landsat 8 Anda menjadi satu kesatuan yang siap diolah.
</p>
</div>

<div class="grid md:grid-cols-2 gap-8 my-8 items-start">
<div class="rounded-xl overflow-hidden shadow-lg border border-white/10">
<img src="/screenshots/tool-manage.png" alt="Antarmuka Tool Manage Landsat" class="w-full" />
</div>
<div class="space-y-4">
<div class="p-4 bg-white/5 rounded-xl border border-white/10">
<h4 class="font-bold text-emerald-400 mb-2">Parameter Input</h4>
<ul class="space-y-3 text-sm">
<li>
<span class="block font-semibold text-white">Output Geodatabase</span>
<span class="text-slate-400">Lokasi penyimpanan dataset (default: GDB proyek Anda).</span>
</li>
<li>
<span class="block font-semibold text-white">Mosaic Name</span>
<span class="text-slate-400">Nama dataset mozaik yang akan dibuat (contoh: <code>L8_Mozaik_2024</code>).</span>
</li>
<li>
<span class="block font-semibold text-white">Input Source Folder</span>
<span class="text-slate-400">Folder tempat Anda menyimpan hasil ekstrak citra Landsat 8. Tool akan mencari file <code>_MTL.txt</code> secara otomatis.</span>
</li>
<li>
<span class="block font-semibold text-white">Dataset Type</span>
<span class="text-slate-400">Pilih <strong>Level 2</strong> (Surface Reflectance) untuk hasil klasifikasi terbaik.</span>
</li>
</ul>
</div>
</div>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="step-3-classify" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🧠 Langkah 3: Klasifikasi Tutupan Lahan</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400">
Tool ini akan membaca input raster Anda dan memprediksi tutupan lahan menggunakan Model Deep Learning (<code>.dlpk</code>). Kini mendukung klasifikasi otomatis ke format Vektor.
</p>
</div>

<div class="my-6 p-4 bg-blue-500/10 border border-blue-500/30 rounded-xl flex flex-col md:flex-row gap-4 items-start md:items-center justify-between">
<div>
<strong class="text-blue-400 block mb-1">⚠️ Wajib Mengunduh Model</strong>
<span class="text-sm text-slate-300">Anda membutuhkan file model pelatihan (.dlpk) untuk menjalankan tool ini.</span>
</div>
<a href="https://drive.google.com/uc?export=download&id=1kAdbTwe7Mk71hILu543uNwc6HRfT3k4H" class="shrink-0 inline-flex items-center gap-2 px-5 py-2.5 bg-blue-600 hover:bg-blue-500 text-white rounded-lg font-semibold transition-all shadow-lg shadow-blue-500/20 no-underline">
<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L9 10.586V3a1 1 0 112 0v7.586l1.293-1.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z" clip-rule="evenodd" /></svg>
Unduh Model (.dlpk)
</a>
</div>

<div class="grid md:grid-cols-2 gap-8 my-8 items-start">
<div class="rounded-xl overflow-hidden shadow-lg border border-white/10">
<img src="/screenshots/tool-classify.png" alt="Antarmuka Tool Klasifikasi" class="w-full" />
</div>
<div class="space-y-4">
<div class="p-4 bg-white/5 rounded-xl border border-white/10">
<h4 class="font-bold text-emerald-400 mb-2">Parameter Utama</h4>
<ul class="space-y-3 text-sm">
<li>
<span class="block font-semibold text-white">Input Raster</span>
<span class="text-slate-400">Raster input (Landsat 8 L2SR).</span>
</li>
<li>
<span class="block font-semibold text-white">File Model (.dlpk)</span>
<span class="text-slate-400">Masukkan file <code>LandCoverClassification.dlpk</code>.</span>
</li>
<li>
<span class="block font-semibold text-white">Convert to Polygon</span>
<span class="text-slate-400">Centang untuk menghasilkan Shapefile secara otomatis.</span>
</li>
<li>
<span class="block font-semibold text-white">Output Standard</span>
<span class="text-slate-400">Pilih <strong>SNI Indonesia (1:50.000)</strong>.</span>
</li>
</ul>
</div>
</div>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="check-license" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🔑 Cek Lisensi & Machine ID</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
<p class="text-slate-400 mb-4">
Untuk melakukan pemesanan lisensi Pro, Anda memerlukan <strong>Machine ID</strong> komputer Anda. Ikuti langkah berikut untuk mendapatkannya:
</p>

<div class="grid md:grid-cols-2 gap-6">
<ol class="space-y-4 text-sm text-slate-300 list-decimal pl-4">
<li class="pl-2">Buka toolbox <strong>Deep Learning Land Cover</strong>.</li>
<li class="pl-2">Klik tool <strong>05. Check License Status</strong>.</li>
<li class="pl-2">Setelah selesai, klik <strong>View Details</strong>.</li>
<li class="pl-2">Salin kode pada baris <strong class="text-white">ID Mesin</strong>.</li>
</ol>
<div class="bg-black/30 rounded-xl p-4 flex items-center justify-center border border-white/5">
<div class="text-center">
<div class="text-xs text-slate-500 mb-2">Contoh Tampilan Output</div>
<div class="font-mono text-emerald-400 text-sm bg-black/50 p-2 rounded border border-white/10">ID Mesin : BFEBFBFF000306A9</div>
</div>
</div>
</div>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="troubleshooting" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">❓ Pemecahan Masalah (Troubleshooting)</h2>

<div class="space-y-4">
<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer">
<summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">GPU Tidak Terdeteksi oleh PyTorch</summary>
<div class="mt-2 text-slate-400 text-sm">
Pastikan Driver NVIDIA terbaru telah terinstal. Jika hardware terdeteksi namun CUDA tidak aktif, silakan instal <strong>CUDA Toolkit 11.8</strong> dan jalankan kembali Tool 01 dengan mode <i>"Force Reinstall All"</i>.
</div>
</details>

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer">
<summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Error: Permission Denied saat Instalasi</summary>
<div class="mt-2 text-slate-400 text-sm">
Gunakan environment hasil <strong>Clone</strong> (seperti DLP-LCL8) untuk menghindari batasan izin akses di folder Program Files.
</div>
</details>

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer">
<summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Hasil Klasifikasi Didominasi Awan/Salju</summary>
<div class="mt-2 text-slate-400 text-sm">
Ini terjadi jika Anda menggunakan data <strong>Level 1 (Digital Number)</strong>. Model ini dilatih khusus untuk data <strong>Collection 2 Level 2 (Surface Reflectance)</strong>.
</div>
</details>

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer">
<summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Masalah Out of Memory (OOM)</summary>
<div class="mt-2 text-slate-400 text-sm">
Kurangi nilai <strong>Batch Size</strong> menjadi <code>1</code> dan <strong>Tile Size</strong> menjadi <code>256</code> pada pengaturan Advanced Klasifikasi.
</div>
</details>
</div>
