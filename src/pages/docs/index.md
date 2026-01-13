---
layout: ../../layouts/DocsLayout.astro
title: Panduan Pengguna & Dokumentasi
---

<p class="text-lg text-slate-300 mb-12 leading-relaxed">
  Selamat datang di dokumentasi resmi <strong class="text-white">Deep Learning Land Cover Toolbox v2.0</strong>. 
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

<h2 id="step-1-libs" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🛠️ Langkah 1: Instalasi Library Pendukung</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
  <p class="text-slate-400 mb-4">
    Setelah toolbox berhasil ditambahkan, langkah pertama yang <strong>wajib</strong> dilakukan adalah menginstal library Python yang dibutuhkan (<em>PyTorch</em> & <em>FastAI</em>). Kami telah menyediakan alat otomatis untuk ini.
  </p>
  <ol class="space-y-3 text-slate-300 list-decimal list-inside marker:text-emerald-500 marker:font-bold">
    <li class="pl-2">Buka tool <strong class="text-white">"03. Auto-Install Deep Learning Libraries"</strong>.</li>
    <li class="pl-2">Tool ini secara otomatis akan:
      <ul class="pl-6 mt-2 space-y-1 list-disc text-slate-400 marker:text-emerald-500/50">
        <li>Mengecek lingkungan Python (<em>environment</em>) Anda.</li>
        <li>Mengunduh library Deep Learning yang kompatibel.</li>
        <li>Mengonfigurasi dukungan GPU (CUDA) jika tersedia.</li>
      </ul>
    </li>
  </ol>
</div>

<div class="flex flex-col md:flex-row gap-8 items-center my-8">
  <div class="w-full md:w-1/2 rounded-xl overflow-hidden shadow-lg border border-white/10">
    <img src="/screenshots/tool-install.png" alt="Antarmuka Tool Install" class="w-full" />
  </div>
  <div class="w-full md:w-1/2 text-sm text-slate-300 space-y-4">
    <div class="p-4 bg-emerald-500/10 border border-emerald-500/20 rounded-lg">
        <strong>Tips Penting:</strong> <br/>
        Untuk instalasi pertama kali, sangat disarankan membuka ArcGIS Pro dengan cara <strong>Klik Kanan > Run as Administrator</strong> agar tidak terjadi masalah izin akses (*permission denied*).
    </div>
    <ul class="space-y-2">
        <li>✅ <strong>Mode Perbaikan:</strong> Pilih "Auto Detect & Fix".</li>
        <li>✅ <strong>Gunakan GPU:</strong> Centang jika Anda memiliki kartu grafis NVIDIA agar proses lebih cepat.</li>
    </ul>
  </div>
</div>

<hr class="border-t border-white/10 my-16" />

<h2 id="step-2-manage" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🛰️ Langkah 2: Persiapan Data (Manage Landsat 8)</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
  <p class="text-slate-400">
    Toolbox ini membutuhkan input berupa <strong>Mosaic Dataset</strong>. Gunakan tool ini untuk merapikan data mentah Landsat 8 Anda menjadi satu kesatuan mozaik yang siap diolah.
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
          <span class="text-slate-400">Lokasi penyimpanan Mosaic Dataset (default: GDB proyek Anda).</span>
        </li>
        <li>
          <span class="block font-semibold text-white">Mosaic Name</span>
          <span class="text-slate-400">Nama dataset mozaik yang akan dibuat (contoh: <code>L8_Mozaik_2024</code>).</span>
        </li>
        <li>
          <span class="block font-semibold text-white">Input Source Folder</span>
          <span class="text-slate-400">Folder tempat Anda menyimpan hasil ekstrak citra Landsat 8. Tool akan mencari file <code>_MTL.txt</code> secara otomatis di dalamnya.</span>
        </li>
        <li>
          <span class="block font-semibold text-white">Dataset Type</span>
          <span class="text-slate-400">Pilih <strong>Level 2</strong> (Surface Reflectance) untuk hasil klasifikasi terbaik.</span>
        </li>
      </ul>
    </div>
  </div>
</div>

> **Catatan:** Pastikan opsi **"Multispectral"** dicentang agar band-band spektral penting ikut terproses.

<hr class="border-t border-white/10 my-16" />

<h2 id="step-3-classify" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🧠 Langkah 3: Klasifikasi Tutupan Lahan</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
  <p class="text-slate-400">
    Ini adalah inti dari toolbox ini. Tool ini akan membaca Mosaic Dataset Anda dan memprediksi tutupan lahan menggunakan Model Deep Learning (<code>.dlpk</code>).
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
  </a>
</div>

<div class="mb-8 p-4 bg-amber-500/10 border border-amber-500/20 rounded-xl flex items-start gap-4">
    <div class="mt-1">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-amber-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
    </div>
    <div>
        <strong class="text-amber-400 block mb-1">PENTING: Syarat Data Input</strong>
        <p class="text-sm text-slate-300 leading-relaxed">
            Tool klasifikasi ini <strong>HANYA BEKERJA</strong> dengan data <strong>Landsat 8 Level 2 (Surface Reflectance)</strong>. 
            Jika Anda menggunakan data Level 1 (Digital Number), hasil klasifikasi akan menjadi tidak valid (seperti terdeteksi sebagai "Snow/Ice" atau "Awan" di seluruh area).
        </p>
    </div>
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
          <span class="text-slate-400">Pilih Mosaic Dataset yang sudah dibuat pada Langkah 2.</span>
        </li>
        <li>
          <span class="block font-semibold text-white">File Model (.dlpk)</span>
          <span class="text-slate-400">Masukkan file <code>LandCoverClassification.dlpk</code> yang sudah Anda unduh.</span>
        </li>
        <li>
          <span class="block font-semibold text-white">Output Raster</span>
          <span class="text-slate-400">Lokasi penyimpanan hasil klasifikasi.</span>
        </li>
        <li>
          <span class="block font-semibold text-white">Convert to Polygon</span>
          <span class="text-slate-400">Centang jika ingin hasil akhir berupa data vektor (Shapefile/Feature Class).</span>
        </li>
      </ul>
    </div>
    
<div class="p-4 bg-white/5 rounded-xl border border-white/10">
  <h4 class="font-bold text-blue-400 mb-2">Pengaturan Lanjutan (Advanced)</h4>
  <ul class="space-y-3 text-sm">
    <li>
       <span class="block font-semibold text-white">Processing Mode</span>
       <span class="text-slate-400">Biarkan default: <code>PROCESS_AS_MOSAICKED_IMAGE</code> untuk menghindari masalah batas antar citra.</span>
    </li>
    <li>
       <span class="block font-semibold text-white">Processor Type</span>
       <span class="text-slate-400">Pilih <strong>GPU</strong> untuk performa maksimal. Gunakan <strong>CPU</strong> hanya jika tidak memiliki GPU NVIDIA.</span>
    </li>
    <li>
       <span class="block font-semibold text-white">Batch Size</span>
       <span class="text-slate-400">Default: <code>4</code>. Turunkan menjadi <code>1</code> jika muncul error <em>"Out of Memory"</em>.</span>
    </li>
  </ul>
</div>
  </div>
</div>

### Kelas Output (Standar SNI)
Tool ini secara otomatis memetakan piksel ke dalam kelas tutupan lahan standar SNI:

<div class="overflow-x-auto">
  <table class="w-full text-left border-collapse rounded-xl overflow-hidden">
    <thead>
      <tr class="bg-white/10 text-white border-b border-white/10">
        <th class="p-4 font-bold text-center w-16">ID</th>
        <th class="p-4 font-bold w-1/4">Nama Kelas</th>
        <th class="p-4 font-bold">Keterangan</th>
      </tr>
    </thead>
    <tbody class="text-sm text-slate-300 divide-y divide-white/5">
      <tr><td class="p-4 text-center font-mono text-emerald-400">1</td><td class="p-4 font-semibold text-white">Air</td><td class="p-4">Badan air, sungai, danau, waduk.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">2</td><td class="p-4 font-semibold text-white">Hutan</td><td class="p-4">Kawasan berhutan dengan tutupan tajuk rapat.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">3</td><td class="p-4 font-semibold text-white">Area Terbuka</td><td class="p-4">Padang rumput atau area terbuka di dalam kawasan hutan.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">4</td><td class="p-4 font-semibold text-white">Rawa</td><td class="p-4">Lahan basah dan vegetasi yang tergenang.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">5</td><td class="p-4 font-semibold text-white">Pertanian</td><td class="p-4">Lahan garapan, sawah, perkebunan rakyat.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">7</td><td class="p-4 font-semibold text-white">Area Terbangun</td><td class="p-4">Kawasan perkotaan, permukiman, jalan raya.</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">8</td><td class="p-4 font-semibold text-white">Lahan Kosong</td><td class="p-4">Tanah terbuka tanpa vegetasi (tanah gundul).</td></tr>
      <tr><td class="p-4 text-center font-mono text-emerald-400">10</td><td class="p-4 font-semibold text-white">Awan</td><td class="p-4">Area tertutup awan (Masking).</td></tr>
    </tbody>
  </table>
</div>


<hr class="border-t border-white/10 my-16" />

<h2 id="check-license" class="text-3xl font-extrabold text-white mb-8 mt-16 scroll-mt-32">🔑 Cek Lisensi & Machine ID</h2>

<div class="bg-white/5 border border-white/10 rounded-2xl p-6 mb-8">
  <p class="text-slate-400 mb-4">
    Untuk melakukan pemesanan lisensi Pro, Anda memerlukan <strong>Machine ID</strong> komputer Anda. Ikuti langkah berikut untuk mendapatkannya:
  </p>
  
  <div class="grid md:grid-cols-2 gap-6">
    <ol class="space-y-4 text-sm text-slate-300 list-decimal pl-4">
      <li class="pl-2">
        Buka ArcGIS Pro dan akses <strong>Catalog Pane</strong>.
      </li>
      <li class="pl-2">
        Buka toolbox <strong>Deep Learning Land Cover</strong>.
      </li>
      <li class="pl-2">
        Klik dua kali pada tool <strong>Check License Status</strong> (ikon kunci).
      </li>
      <li class="pl-2">
        Klik <strong>Run</strong> tanpa mengubah parameter apapun.
      </li>
      <li class="pl-2">
        Setelah selesai, klik <strong>View Details</strong> pada jendela hasil.
      </li>
      <li class="pl-2">
        Salin kode unik yang tertera pada baris <strong>ID Mesin</strong>.
      </li>
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

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer">
    <summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Gagal Install / Permission Denied</summary>
    <div class="mt-2 text-slate-400 text-sm">
        Tutup aplikasi ArcGIS Pro sepenuhnya. Klik kanan shortcut ArcGIS Pro dan pilih <strong>"Run as Administrator"</strong>. Lalu jalankan tool Instalasi kembali.
    </div>
</details>

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer mt-4">
    <summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Hasil Klasifikasi "Snow/Ice" Semua</summary>
    <div class="mt-2 text-slate-400 text-sm">
        Ini terjadi jika Anda menggunakan data <strong>Level 1 (DN)</strong> pada model yang dilatih untuk <strong>Level 2</strong>. Pastikan Anda menggunakan data Landsat 8 Collection 2 Level 2 (Surface Reflectance) agar nilai spektralnya sesuai.
    </div>
</details>

<details class="group bg-white/5 border border-white/10 rounded-xl p-4 cursor-pointer mt-4">
    <summary class="font-bold text-white group-hover:text-emerald-400 transition-colors">Error: CUDA Out of Memory</summary>
    <div class="mt-2 text-slate-400 text-sm">
        Pada tool Klasifikasi, buka bagian <strong>Advanced Parameters</strong> dan kurangi nilai <strong>Batch Size</strong> menjadi <code>1</code>.
    </div>
</details>
