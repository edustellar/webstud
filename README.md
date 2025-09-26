<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EDULINK</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* Pengaturan untuk mencegah scroll horizontal */
        html, body {
            width: 100%;
            overflow-x: hidden;
        }
        html { scroll-behavior: smooth; }
        body { font-family: 'Inter', sans-serif; background-color: #f1f5f9; }
        .dark body { background-color: #0f172a; }
        
        /* Main page visibility & transition */
        .main-content > .page { display: none; transition: opacity 0.3s ease-in-out; }
        .main-content > .page.active { display: block; }

        /* Auth Page Transition Styles */
        #authContainer { position: relative; width: 100vw; height: 100vh; overflow-x: hidden;}
        .auth-page {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease-in-out;
            visibility: hidden;
        }
        .auth-page.active {
            opacity: 1;
            pointer-events: auto;
            visibility: visible;
        }

        .sidebar-link.active { background-color: #0ea5e9; color: white; font-weight: 600; }
        .sidebar-link.active i { color: white; }
        .form-select {
            -webkit-appearance: none; -moz-appearance: none; appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24' fill='none' stroke='%2364748b' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='m6 9 6 6 6-6'/%3E%3C/svg%3E");
            background-repeat: no-repeat; background-position: right 0.75rem center; background-size: 1.25em;
        }
        .dark .form-select { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24' fill='none' stroke='%239ca3af' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='m6 9 6 6 6-6'/%3E%3C/svg%3E"); }
        .feature-card { transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out; }
        .feature-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(14, 165, 233, 0.1), 0 4px 6px -2px rgba(14, 165, 233, 0.05); }
        #app-wrapper.feature-view nav { display: none; }
        #app-wrapper.feature-view main { padding: 0; }
        .custom-notification { transition: opacity 0.3s, transform 0.3s; }
        #shareModal, #profileModal { transition: opacity 0.3s ease; }
        .modal-content { transition: transform 0.3s ease; }
        
        /* Favorite heart icon style */
        .favorite-btn i { transition: all 0.2s ease-in-out; }
        .favorite-btn.favorited i { fill: #ef4444; color: #ef4444; }
    </style>
</head>
<body class="bg-slate-100 dark:bg-slate-900">

    <!-- Auth Pages -->
    <div id="authContainer">
        <!-- Halaman Register -->
        <div id="registerPage" class="auth-page active grid lg:grid-cols-2 h-screen w-full">
             <div class="flex items-center justify-center bg-slate-50 p-4">
                <div class="w-full max-w-md bg-white shadow-xl rounded-2xl p-8">
                    <h1 class="text-3xl font-bold text-gray-800 mb-2">Buat Akun Baru</h1>
                    <p class="text-slate-500 mb-6">Gabung dan mulai perjalanan belajarmu!</p>
                    <form onsubmit="event.preventDefault(); showAuthPage('loginPage'); showNotification('Pendaftaran berhasil! Silakan login.', 'success');" class="space-y-4">
                        <div class="grid grid-cols-2 gap-4">
                            <div><label class="block text-sm font-medium text-slate-600">Nama Depan</label><input type="text" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500"></div>
                            <div><label class="block text-sm font-medium text-slate-600">Nama Belakang</label><input type="text" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500"></div>
                        </div>
                        <div><label class="block text-sm font-medium text-slate-600">Alamat Email</label><input type="email" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500"></div>
                        <div><label class="block text-sm font-medium text-slate-600">Buat Sandi</label><input type="password" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500"></div>
                        <div><label class="block text-sm font-medium text-slate-600">Konfirmasi Sandi</label><input type="password" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500"></div>
                        <button type="submit" class="w-full bg-sky-500 text-white font-semibold py-3 px-4 rounded-lg hover:bg-sky-600">Daftar</button>
                    </form>
                     <p class="text-center text-sm text-slate-500 mt-6">Sudah punya akun? <a href="#" onclick="showAuthPage('loginPage')" class="font-semibold text-sky-500 hover:text-sky-600">Masuk di sini</a></p>
                </div>
            </div>
             <div class="hidden lg:flex flex-col items-center justify-center bg-blue-800 text-white p-12 text-center">
                 <h1 class="text-6xl font-extrabold tracking-wider">EDULINK</h1>
                 <p class="mt-4 text-lg text-blue-200">Satu Akun untuk Semua Kebutuhan Belajarmu.</p>
                 <i data-lucide="rocket" class="w-48 h-48 mt-12 text-blue-600"></i>
            </div>
        </div>
        <!-- Halaman Login -->
        <div id="loginPage" class="auth-page grid lg:grid-cols-2 h-screen w-full">
            <div class="hidden lg:flex flex-col items-center justify-center bg-blue-800 text-white p-12 text-center">
                 <h1 class="text-6xl font-extrabold tracking-wider">EDULINK</h1>
                 <p class="mt-4 text-lg text-blue-200">Gerbang Menuju Potensi Akademik Terbaikmu.</p>
                 <i data-lucide="graduation-cap" class="w-48 h-48 mt-12 text-blue-600"></i>
            </div>
            <div class="flex items-center justify-center bg-slate-50 p-4">
                <div class="w-full max-w-md bg-white shadow-xl rounded-2xl p-8">
                    <h1 class="text-3xl font-bold text-gray-800 mb-2">Selamat Datang Kembali</h1>
                    <p class="text-slate-500 mb-8">Mulai langkahmu, temukan solusi terbaik.</p>
                    <form onsubmit="event.preventDefault(); login();" class="space-y-4">
                        <div>
                            <label for="login-email" class="block text-sm font-medium text-slate-600">Alamat Email</label>
                            <input type="email" id="login-email" value="user@edulink.com" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500">
                        </div>
                        <div>
                            <label for="login-password" class="block text-sm font-medium text-slate-600">Kata Sandi</label>
                            <input type="password" id="login-password" value="password123" required class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500">
                        </div>
                        <button type="submit" class="w-full bg-sky-500 text-white font-semibold py-3 px-4 rounded-lg hover:bg-sky-600 transition-transform hover:scale-[1.02]">Masuk</button>
                    </form>
                    <p class="text-center text-sm text-slate-500 mt-6">
                        Belum punya akun? <a href="#" onclick="showAuthPage('registerPage')" class="font-semibold text-sky-500 hover:text-sky-600">Daftar di sini</a>
                    </p>
                </div>
            </div>
        </div>
    </div>

    <!-- App Wrapper -->
    <div id="app-wrapper" class="flex h-screen hidden">
        <!-- Sidebar -->
        <nav class="w-64 bg-white dark:bg-slate-800 shadow-lg flex-col hidden md:flex transition-colors">
            <div class="p-6 text-center border-b dark:border-slate-700"><h1 class="text-3xl font-extrabold tracking-wider text-blue-800 dark:text-white">EDULINK</h1></div>
            <div class="flex-grow p-4 space-y-2">
                <a href="#" onclick="showPage('berandaPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors active"><i data-lucide="layout-dashboard" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Beranda</a>
                <a href="#" onclick="showPage('chatPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="message-circle" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Chat</a>
                <a href="#" onclick="showPage('langgananPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="gem" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Langganan</a>
                <a href="#" onclick="showPage('promoPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="ticket" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Promo</a>
                <a href="#" onclick="showPage('favoritPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="heart" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Favorit</a>
                <a href="#" onclick="showPage('rewardPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="star" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Poin & Hadiah</a>
                <a href="#" onclick="showPage('kuisionerPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="clipboard-list" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Isi Kuisioner</a>
                <a href="#" onclick="showPage('mentorRegisterPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="user-plus" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Daftar Jadi Mentor</a>
                <a href="#" onclick="showPage('mentorDashboardPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="bar-chart-3" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> Dashboard Mentor</a>
                <a href="#" onclick="showPage('faqPage', this)" class="sidebar-link flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-sky-100 dark:hover:bg-slate-700 transition-colors"><i data-lucide="help-circle" class="w-5 h-5 mr-3 text-slate-500 dark:text-slate-400"></i> FAQ</a>
            </div>
            <div class="p-4 border-t dark:border-slate-700"><a href="#" onclick="logout()" class="flex items-center p-3 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-red-50 dark:hover:bg-red-900/20 transition-colors"><i data-lucide="log-out" class="w-5 h-5 mr-3 text-red-500"></i> Logout</a></div>
        </nav>

        <!-- Main Content -->
        <main class="flex-1 p-8 overflow-y-auto main-content transition-colors">
            <div id="berandaPage" class="page active">
                 <div class="flex justify-between items-center mb-8">
                    <h1 class="text-3xl font-bold text-gray-800 dark:text-white">Selamat Datang, Rifki!</h1>
                    <div class="flex items-center gap-4">
                         <div class="bg-amber-100 text-amber-800 font-bold flex items-center gap-2 px-4 py-2 rounded-full">
                            <i data-lucide="star" class="w-5 h-5"></i>
                            <span id="userPoints">1,250 Poin</span>
                        </div>
                        <button id="theme-toggle" type="button" class="text-slate-500 dark:text-slate-400 hover:bg-slate-200 dark:hover:bg-slate-700 rounded-full text-sm p-2.5">
                            <i data-lucide="moon" id="theme-toggle-dark-icon" class="w-5 h-5 hidden"></i>
                            <i data-lucide="sun" id="theme-toggle-light-icon" class="w-5 h-5 hidden"></i>
                        </button>
                    </div>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div onclick="setupFeaturePage('consulink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700"><div class="bg-emerald-100 dark:bg-emerald-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="messages-square" class="w-10 h-10 text-emerald-500"></i></div><h3 class="text-xl font-bold text-blue-800 dark:text-white">Consulink</h3></div>
                    <div onclick="setupFeaturePage('paperlink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700"><div class="bg-violet-100 dark:bg-violet-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="file-text" class="w-10 h-10 text-violet-500"></i></div><h3 class="text-xl font-bold text-blue-800 dark:text-white">Paperlink</h3></div>
                    <div onclick="setupFeaturePage('courselink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700"><div class="bg-amber-100 dark:bg-amber-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="book-open" class="w-10 h-10 text-amber-500"></i></div><h3 class="text-xl font-bold text-blue-800 dark:text-white">Courselink</h3></div>
                    <div onclick="setupFeaturePage('complink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700"><div class="bg-rose-100 dark:bg-rose-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="trophy" class="w-10 h-10 text-rose-500"></i></div><h3 class="text-xl font-bold text-blue-800 dark:text-white">Complink</h3></div>
                    <div onclick="showPage('sourcelinkPage', this)" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700 lg:col-span-1 sm:col-span-2 lg:col-start-2">
                        <div class="bg-teal-100 dark:bg-teal-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="users" class="w-10 h-10 text-teal-500"></i></div>
                        <h3 class="text-xl font-bold text-blue-800 dark:text-white">Sourcelink</h3>
                    </div>
                </div>
                 <div id="hot-services-container" class="mt-10 bg-white dark:bg-slate-800 dark:border-slate-700 p-6 rounded-xl border"></div>
                 <div id="testimonials-container" class="mt-10"></div>
            </div>

            <div id="chatPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-6">Riwayat Chat Mentor</h1>
                <div class="bg-white dark:bg-slate-800 dark:border-slate-700 p-6 rounded-xl border space-y-4">
                    <div onclick="showNotification('Layanan chat dengan mentor ini telah berakhir', 'info')" class="flex items-center p-3 rounded-lg hover:bg-slate-50 dark:hover:bg-slate-700 cursor-pointer"><img src="https://placehold.co/48x48/fecaca/b91c1c?text=A" class="rounded-full w-12 h-12 mr-4"><div class="flex-grow"><p class="font-semibold dark:text-white">Anisa Putri</p><p class="text-sm text-slate-500 dark:text-slate-400">Bisa tolong review bagian pendahuluan...</p></div><span class="text-xs text-slate-400 dark:text-slate-500">2 hari lalu</span></div>
                    <div onclick="showNotification('Layanan chat dengan mentor ini telah berakhir', 'info')" class="flex items-center p-3 rounded-lg hover:bg-slate-50 dark:hover:bg-slate-700 cursor-pointer"><img src="https://placehold.co/48x48/bae6fd/1e3a8a?text=B" class="rounded-full w-12 h-12 mr-4"><div class="flex-grow"><p class="font-semibold dark:text-white">Budi Santoso</p><p class="text-sm text-slate-500 dark:text-slate-400">Oke, terima kasih atas bantuannya!</p></div><span class="text-xs text-slate-400 dark:text-slate-500">5 hari lalu</span></div>
                    <div onclick="showNotification('Layanan chat dengan mentor ini telah berakhir', 'info')" class="flex items-center p-3 rounded-lg hover:bg-slate-50 dark:hover:bg-slate-700 cursor-pointer"><img src="https://placehold.co/48x48/d8b4fe/7e22ce?text=C" class="rounded-full w-12 h-12 mr-4"><div class="flex-grow"><p class="font-semibold dark:text-white">Citra Lestari</p><p class="text-sm text-slate-500 dark:text-slate-400">Untuk soal ONMIPA, kita bisa mulai...</p></div><span class="text-xs text-slate-400 dark:text-slate-500">1 minggu lalu</span></div>
                    <div onclick="showNotification('Layanan chat dengan mentor ini telah berakhir', 'info')" class="flex items-center p-3 rounded-lg hover:bg-slate-50 dark:hover:bg-slate-700 cursor-pointer"><img src="https://placehold.co/48x48/a5f3fc/0e7490?text=D" class="rounded-full w-12 h-12 mr-4"><div class="flex-grow"><p class="font-semibold dark:text-white">Dewi Anggraini</p><p class="text-sm text-slate-500 dark:text-slate-400">Tentu, saya siap membantu soal manajemen...</p></div><span class="text-xs text-slate-400 dark:text-slate-500">2 minggu lalu</span></div>
                </div>
            </div>

            <div id="langgananPage" class="page">
                 <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-2">Paket Langganan</h1>
                <p class="text-slate-500 dark:text-slate-400 mb-6">Pilih paket terbaik untuk memaksimalkan potensimu!</p>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="border-2 border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 rounded-xl p-6 text-center flex flex-col"><h3 class="text-xl font-bold dark:text-white">Paket Hemat</h3><p class="text-sm text-slate-500 dark:text-slate-400 mb-4">5x Transaksi (1 Fitur)</p><p class="text-lg font-medium text-slate-400 dark:text-slate-500 line-through">Rp 30.000</p><p class="text-4xl font-extrabold text-blue-800 dark:text-white mb-6">Rp 24.000</p><button onclick="showPaymentPage({type: 'Paket', name: 'Paket Hemat', price: '24000'})" class="mt-auto w-full bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Pilih Paket</button></div>
                    <div class="border-2 border-sky-500 bg-white dark:bg-slate-800 rounded-xl p-6 text-center relative flex flex-col"><div class="absolute top-0 -translate-y-1/2 left-1/2 -translate-x-1/2 bg-sky-500 text-white text-xs font-bold px-3 py-1 rounded-full">PALING LARIS</div><h3 class="text-xl font-bold dark:text-white">Paket Puas</h3><p class="text-sm text-slate-500 dark:text-slate-400 mb-4">10x Transaksi (1 Fitur)</p><p class="text-lg font-medium text-slate-400 dark:text-slate-500 line-through">Rp 60.000</p><p class="text-4xl font-extrabold text-blue-800 dark:text-white mb-6">Rp 45.000</p><button onclick="showPaymentPage({type: 'Paket', name: 'Paket Puas', price: '45000'})" class="mt-auto w-full bg-sky-500 text-white font-semibold py-2 px-4 rounded-lg hover:bg-sky-600">Pilih Paket</button></div>
                    <div class="border-2 border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800 rounded-xl p-6 text-center flex flex-col"><h3 class="text-xl font-bold dark:text-white">Paket Sultan</h3><p class="text-sm text-slate-500 dark:text-slate-400 mb-4">20x Transaksi (Bebas pilih Fitur)</p><p class="text-lg font-medium text-slate-400 dark:text-slate-500 line-through">Rp 121.000</p><p class="text-4xl font-extrabold text-blue-800 dark:text-white mb-6">Rp 85.000</p><button onclick="showPaymentPage({type: 'Paket', name: 'Paket Sultan', price: '85000'})" class="mt-auto w-full bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Pilih Paket</button></div>
                </div>
            </div>

            <div id="promoPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-6">Promo Spesial Untukmu</h1>
                <div class="space-y-6">
                    <div class="bg-gradient-to-r from-blue-800 to-sky-500 text-white p-8 rounded-xl flex justify-between items-center"><div><h3 class="text-2xl font-bold">Diskon Pengguna Pertama!</h3><p class="opacity-80">Dapatkan potongan 50% untuk transaksi pertamamu.</p></div><button onclick="showNotification('Diskon didapatkan!', 'success')" class="bg-white text-blue-800 font-bold py-2 px-6 rounded-lg">Klaim</button></div>
                    <div class="bg-white dark:bg-slate-800 border dark:border-slate-700 p-6 rounded-xl flex justify-between items-center"><div><h3 class="text-xl font-bold dark:text-white">Ajak Teman, Dapat Cuan!</h3><p class="text-slate-500 dark:text-slate-400">Bagikan kode referral dan dapatkan diskon 25%.</p></div><button onclick="openShareModal()" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Bagikan</button></div>
                    <div class="bg-white dark:bg-slate-800 border dark:border-slate-700 p-6 rounded-xl flex justify-between items-center"><div><h3 class="text-xl font-bold dark:text-white">Promo Hari Pendidikan</h3><p class="text-slate-500 dark:text-slate-400">Diskon 20% untuk semua layanan Paperlink. Terbatas!</p></div><button onclick="showNotification('Promo berhasil diklaim!', 'success')" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Klaim</button></div>
                    <div class="bg-white dark:bg-slate-800 border dark:border-slate-700 p-6 rounded-xl flex justify-between items-center"><div><h3 class="text-xl font-bold dark:text-white">Cashback E-Wallet</h3><p class="text-slate-500 dark:text-slate-400">Dapatkan cashback 10% untuk pembayaran via GoPay/OVO.</p></div><button onclick="showPage('promoDetailPage')" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Lihat Detail</button></div>
                </div>
            </div>

            <div id="favoritPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-6">Mentor Favorit</h1>
                <div id="favoriteMentorList" class="space-y-4">
                    <div class="bg-white dark:bg-slate-800 p-12 rounded-xl border dark:border-slate-700 text-center"><i data-lucide="folder-heart" class="w-16 h-16 mx-auto text-slate-300 dark:text-slate-600 mb-4"></i><h3 class="text-xl font-semibold dark:text-white">Belum Ada Favorit</h3><p class="text-slate-500 dark:text-slate-400 mt-1">Tandai mentor yang kamu sukai untuk akses lebih cepat!</p></div>
                </div>
            </div>

             <div id="rewardPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-2">Poin & Hadiah</h1>
                <p class="text-slate-500 dark:text-slate-400 mb-6">Tukarkan poin yang kamu kumpulkan dengan hadiah menarik!</p>
                <div class="bg-gradient-to-r from-amber-400 to-yellow-500 text-white p-6 rounded-xl mb-8 flex justify-between items-center">
                    <div>
                        <p class="text-sm opacity-80">Total Poin Kamu</p>
                        <p class="text-4xl font-bold">1,250</p>
                    </div>
                    <i data-lucide="gift" class="w-12 h-12 opacity-50"></i>
                </div>
                 <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700">
                        <h3 class="font-bold dark:text-white">Diskon 10% Consulink</h3>
                        <p class="text-sm text-slate-500 dark:text-slate-400">Gunakan untuk 1x sesi Consulink</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="font-bold text-amber-600">500 Poin</span>
                            <button onclick="showNotification('Hadiah berhasil ditukar!', 'success')" class="bg-amber-500 text-white text-sm font-semibold py-1 px-3 rounded-md">Tukar</button>
                        </div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700">
                        <h3 class="font-bold dark:text-white">Potongan Rp 5.000</h3>
                        <p class="text-sm text-slate-500 dark:text-slate-400">Berlaku untuk semua layanan</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="font-bold text-amber-600">1000 Poin</span>
                            <button onclick="showNotification('Hadiah berhasil ditukar!', 'success')" class="bg-amber-500 text-white text-sm font-semibold py-1 px-3 rounded-md">Tukar</button>
                        </div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700">
                        <h3 class="font-bold dark:text-white">Gratis 1x Sesi Complink</h3>
                        <p class="text-sm text-slate-500 dark:text-slate-400">Mentoring lomba (maks. 1 jam)</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="font-bold text-amber-600">2500 Poin</span>
                            <button class="bg-slate-200 dark:bg-slate-700 text-slate-500 dark:text-slate-400 text-sm font-semibold py-1 px-3 rounded-md cursor-not-allowed">Poin Kurang</button>
                        </div>
                    </div>
                </div>
            </div>
            
             <div id="kuisionerPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-2">Isi Kuisioner</h1>
                <p class="text-slate-500 dark:text-slate-400 mb-6">Bantu penelitian dan dapatkan hadiah menarik!</p>
                <div class="space-y-4">
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Pengaruh Media Sosial Terhadap Minat Belajar Mahasiswa</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Universitas Gadjah Mada</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 100</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Analisis Pola Tidur dan Tingkat Stres pada Pekerja Remote</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Fakultas Psikologi UI</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 120</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Preferensi Konsumen Terhadap Produk Ramah Lingkungan</h3><p class="text-sm text-slate-500 dark:text-slate-400">Riset oleh Startup Greenly</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 110</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Dampak Penggunaan E-Wallet di Kalangan Generasi Z</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Institut Teknologi Bandung</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 115</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Studi Kelayakan Bisnis Coffee Shop di Area Urban</h3><p class="text-sm text-slate-500 dark:text-slate-400">Riset oleh Universitas Brawijaya</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 105</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Persepsi Mahasiswa Terhadap Pembelajaran Daring</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Universitas Negeri Yogyakarta</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 100</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Efektivitas Iklan di Platform Streaming Video</h3><p class="text-sm text-slate-500 dark:text-slate-400">Riset oleh Agensi Pemasaran Digital</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 120</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Hubungan Antara Aktivitas Fisik dan Kesehatan Mental</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Fakultas Kedokteran Unpad</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 110</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Minat Baca Buku Fisik di Era Digital</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh Komunitas Literasi Nasional</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 100</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Penggunaan Transportasi Publik vs. Kendaraan Pribadi</h3><p class="text-sm text-slate-500 dark:text-slate-400">Survei oleh Dinas Perhubungan Kota</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 115</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Perilaku Belanja Online Selama Periode Diskon</h3><p class="text-sm text-slate-500 dark:text-slate-400">Riset oleh Asosiasi E-commerce Indonesia</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 120</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Tingkat Kepuasan Pengguna Aplikasi Mobile Banking</h3><p class="text-sm text-slate-500 dark:text-slate-400">Survei Internal Bank ABC</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 100</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Gaya Hidup Minimalis di Kalangan Milenial</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian Sosiologi Universitas Airlangga</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 110</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Kebutuhan Fitur Baru pada Aplikasi Streaming Musik</h3><p class="text-sm text-slate-500 dark:text-slate-400">Riset UX oleh Tim Produk NadaStream</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 105</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-5 rounded-xl border dark:border-slate-700 flex justify-between items-center">
                        <div><h3 class="font-bold dark:text-white">Pola Konsumsi Kopi di kalangan Mahasiswa Akhir</h3><p class="text-sm text-slate-500 dark:text-slate-400">Penelitian oleh IPB University</p></div>
                        <div class="text-right"><p class="font-semibold text-green-600 dark:text-green-400">Reward: Rp 110</p><button onclick="showNotification('Membuka kuisioner...','info')" class="text-sm font-semibold text-sky-600 dark:text-sky-400 mt-1">Mulai Isi</button></div>
                    </div>
                </div>
            </div>

            <div id="sourcelinkPage" class="page">
                <div id="sourcelinkStep1">
                    <h1 class="text-3xl font-bold text-gray-800 dark:text-white">Cari Responden (Sourcelink)</h1>
                    <p class="text-slate-500 dark:text-slate-400 mb-6">Tentukan kriteria responden yang Anda butuhkan untuk penelitian Anda.</p>
                    <div class="bg-white dark:bg-slate-800 p-8 rounded-xl border dark:border-slate-700">
                        <form id="sourcelinkCriteriaForm" class="space-y-6">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                <div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Rentang Usia</label><select class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm dark:text-white"><option>17-20 tahun</option><option>21-25 tahun</option><option>26-30 tahun</option><option>31-40 tahun</option><option>40+ tahun</option></select></div>
                                <div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Jenis Kelamin</label><select class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm dark:text-white"><option>Semua</option><option>Laki-laki</option><option>Perempuan</option></select></div>
                                <div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Tingkat Penghasilan</label><select class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm dark:text-white"><option>&lt; Rp 3.000.000</option><option>Rp 3.000.000 - Rp 5.000.000</option><option>Rp 5.000.000 - Rp 10.000.000</option><option>&gt; Rp 10.000.000</option><option>Tidak Berpenghasilan / Pelajar</option></select></div>
                                <div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Pendidikan Terakhir</label><select class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm dark:text-white"><option>Semua</option><option>SMA/Sederajat</option><option>Diploma (D1/D2/D3)</option><option>Sarjana (S1)</option><option>Magister/Doktor (S2/S3)</option></select></div>
                            </div>
                            <div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Kriteria Lainnya (Opsional)</label><textarea placeholder="Contoh: Mahasiswa aktif, berdomisili di Jabodetabek, pengguna e-commerce..." class="mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500 dark:text-white" rows="3"></textarea></div>
                            <button type="button" onclick="showSourcelinkStep2()" class="w-full bg-sky-500 text-white font-semibold py-3 px-4 rounded-lg hover:bg-sky-600">Lanjutkan ke Penyebaran Kuisioner</button>
                        </form>
                    </div>
                </div>
                 <div id="sourcelinkStep2" class="hidden">
                    <header class="flex items-center mb-6"><button onclick="resetSourcelinkPage()" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button><h1 class="text-3xl font-bold text-gray-800 dark:text-white">Sebar Kuisioner</h1></header>
                    <div class="bg-white dark:bg-slate-800 p-8 rounded-xl border dark:border-slate-700">
                        <form id="sourcelinkLinkForm" onsubmit="event.preventDefault(); submitSourcelink();">
                            <label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Link Kuisioner Anda</label>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mb-2">Pastikan link dapat diakses secara publik. Kami mendukung Google Forms, SurveyMonkey, dll.</p>
                            <input type="url" placeholder="https://docs.google.com/forms/..." required class="mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md shadow-sm focus:outline-none focus:ring-sky-500 focus:border-sky-500 dark:text-white">
                            <button type="submit" class="mt-6 w-full bg-sky-500 text-white font-semibold py-3 px-4 rounded-lg hover:bg-sky-600">Sebar Kuisioner Sekarang</button>
                        </form>
                    </div>
                </div>
                <div id="sourcelinkSuccess" class="hidden text-center bg-white dark:bg-slate-800 p-12 rounded-xl border dark:border-slate-700">
                    <i data-lucide="send" class="w-16 h-16 mx-auto text-green-500 mb-4"></i>
                    <h2 class="text-2xl font-bold dark:text-white">Kuisioner Diterima!</h2>
                    <p class="text-slate-500 dark:text-slate-400 mt-2 max-w-xl mx-auto">Kuisioner Anda telah kami terima dan akan segera disebar kepada responden yang sesuai. Anda akan menerima notifikasi melalui email jika target responden telah tercapai.</p>
                    <button onclick="showPage('berandaPage')" class="mt-6 bg-sky-500 text-white font-semibold py-2 px-6 rounded-lg">Kembali ke Beranda</button>
                </div>
            </div>

            <div id="mentorRegisterPage" class="page">
                 <div id="mentorRegisterSelection">
                     <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-2">Daftar Menjadi Mitra Mentor</h1>
                     <p class="text-slate-500 dark:text-slate-400 mb-6">Pilih kategori yang paling sesuai dengan keahlianmu.</p>
                     <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div onclick="showMentorRegisterForm('Consulink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700">
                            <div class="bg-emerald-100 dark:bg-emerald-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="messages-square" class="w-10 h-10 text-emerald-500"></i></div>
                            <h3 class="text-xl font-bold text-blue-800 dark:text-white">Mentor Consulink</h3>
                            <p class="text-sm text-slate-500 dark:text-slate-400 mt-2">Bimbingan akademik, tugas, ujian, dan kehidupan kampus.</p>
                            <p class="text-xs font-semibold text-sky-600 dark:text-sky-400 mt-2">Syarat: Minimal semester 5</p>
                        </div>
                        <div onclick="showMentorRegisterForm('Paperlink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700">
                            <div class="bg-violet-100 dark:bg-violet-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="file-text" class="w-10 h-10 text-violet-500"></i></div>
                            <h3 class="text-xl font-bold text-blue-800 dark:text-white">Mentor Paperlink</h3>
                            <p class="text-sm text-slate-500 dark:text-slate-400 mt-2">Bimbingan karya tulis ilmiah, metodologi, analisis data, dan publikasi.</p>
                             <p class="text-xs font-semibold text-sky-600 dark:text-sky-400 mt-2">Syarat: Minimal S1</p>
                        </div>
                        <div onclick="showMentorRegisterForm('Courselink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700">
                            <div class="bg-amber-100 dark:bg-amber-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="book-open" class="w-10 h-10 text-amber-500"></i></div>
                            <h3 class="text-xl font-bold text-blue-800 dark:text-white">Mentor Courselink</h3>
                            <p class="text-sm text-slate-500 dark:text-slate-400 mt-2">Les privat atau kolektif untuk mata kuliah spesifik.</p>
                            <p class="text-xs font-semibold text-sky-600 dark:text-sky-400 mt-2">Syarat: Minimal semester 5</p>
                        </div>
                        <div onclick="showMentorRegisterForm('Complink')" class="feature-card bg-white dark:bg-slate-800 p-6 rounded-xl text-center cursor-pointer border dark:border-slate-700">
                            <div class="bg-rose-100 dark:bg-rose-900/50 rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4"><i data-lucide="trophy" class="w-10 h-10 text-rose-500"></i></div>
                            <h3 class="text-xl font-bold text-blue-800 dark:text-white">Mentor Complink</h3>
                             <p class="text-sm text-slate-500 dark:text-slate-400 mt-2">Mentoring persiapan berbagai macam lomba akademik.</p>
                             <p class="text-xs font-semibold text-sky-600 dark:text-sky-400 mt-2">Syarat: Minimal semester 5</p>
                        </div>
                     </div>
                 </div>

                <div id="mentorRegisterFormContainer" class="hidden">
                    <header class="flex items-center mb-6">
                        <button onclick="showMentorRegisterSelection()" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button>
                        <h1 id="mentorRegisterFormTitle" class="text-3xl font-bold text-gray-800 dark:text-white">Formulir Pendaftaran Mentor</h1>
                    </header>
                    <div class="bg-white dark:bg-slate-800 border dark:border-slate-700 p-8 rounded-xl">
                        <form onsubmit="event.preventDefault(); submitMentorForm()" class="space-y-6">
                             <p class="text-sm text-slate-500 dark:text-slate-400 bg-slate-100 dark:bg-slate-700 p-4 rounded-lg">Lengkapi data dirimu dengan benar. Tim kami akan meninjau pendaftaranmu dan memberikan status pendaftaran melalui email.</p>
                            <div class="grid md:grid-cols-2 gap-6">
                                <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Nama Lengkap</label><input type="text" required class="mt-1 w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md dark:text-white"></div>
                                <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Email</label><input type="email" required class="mt-1 w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md dark:text-white"></div>
                                <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Asal Universitas</label><input type="text" required class="mt-1 w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md dark:text-white"></div>
                                <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Jurusan</label><input type="text" required class="mt-1 w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md dark:text-white"></div>
                            </div>
                            <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Link Portofolio (LinkedIn, Google Drive, dll)</label><input type="url" placeholder="https://..." required class="mt-1 w-full px-3 py-2 bg-white dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md dark:text-white"></div>
                             <div><label class="block text-sm font-medium text-slate-700 dark:text-slate-300">Unggah CV (PDF, maks 2MB)</label><input type="file" accept=".pdf" required class="mt-1 block w-full text-sm text-slate-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-sky-50 dark:file:bg-slate-600 file:text-sky-700 dark:file:text-sky-300 hover:file:bg-sky-100 dark:hover:file:bg-slate-500"/></div>
                            <div class="pt-4">
                                <button type="submit" class="w-full bg-sky-500 text-white font-semibold py-3 rounded-lg hover:bg-sky-600">Kirim Pendaftaran</button>
                            </div>
                        </form>
                    </div>
                </div>
                
                <div id="mentorRegisterSuccess" class="hidden text-center bg-white dark:bg-slate-800 p-12 rounded-xl border dark:border-slate-700">
                    <i data-lucide="check-circle-2" class="w-16 h-16 mx-auto text-green-500 mb-4"></i>
                    <h2 class="text-2xl font-bold dark:text-white">Pendaftaran Terkirim!</h2>
                    <p class="text-slate-500 dark:text-slate-400 mt-2 max-w-xl mx-auto">Pendaftaran mitra mentor telah kami terima. Tim EDULINK akan meninjau datamu dan menghubungimu segera melalui email untuk memberikan status pendaftaran.</p>
                    <button onclick="showPage('berandaPage')" class="mt-6 bg-sky-500 text-white font-semibold py-2 px-6 rounded-lg">Kembali ke Beranda</button>
                </div>
            </div>
            
             <div id="mentorDashboardPage" class="page">
                <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-6">Dashboard Mentor</h1>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                    <div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700 flex items-center gap-4">
                        <div class="bg-blue-100 dark:bg-blue-900/50 p-3 rounded-full"><i data-lucide="users" class="w-8 h-8 text-blue-500"></i></div>
                        <div><p class="text-sm text-slate-500 dark:text-slate-400">Total Sesi Bulan Ini</p><p class="text-2xl font-bold dark:text-white">57</p></div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700 flex items-center gap-4">
                        <div class="bg-amber-100 dark:bg-amber-900/50 p-3 rounded-full"><i data-lucide="star" class="w-8 h-8 text-amber-500"></i></div>
                        <div><p class="text-sm text-slate-500 dark:text-slate-400">Rating Rata-Rata</p><p class="text-2xl font-bold dark:text-white">4.9 / 5.0</p></div>
                    </div>
                     <div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700 flex items-center gap-4">
                        <div class="bg-green-100 dark:bg-green-900/50 p-3 rounded-full"><i data-lucide="dollar-sign" class="w-8 h-8 text-green-500"></i></div>
                        <div><p class="text-sm text-slate-500 dark:text-slate-400">Pendapatan Bulan Ini</p><p class="text-2xl font-bold dark:text-white">Rp 832.000</p></div>
                    </div>
                </div>
                <div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700">
                    <h2 class="text-xl font-bold dark:text-white mb-4">Sesi Mendatang</h2>
                    <div class="space-y-3">
                        <div class="bg-slate-50 dark:bg-slate-700 p-4 rounded-lg flex justify-between items-center">
                            <div><p class="font-semibold dark:text-white">Budi (Courselink: Kalkulus)</p><p class="text-sm text-slate-500 dark:text-slate-400">25 September 2025, 14:00 WIB</p></div>
                            <a href="#" class="text-sm font-semibold text-sky-600 dark:text-sky-400">Lihat Detail</a>
                        </div>
                        <div class="bg-slate-50 dark:bg-slate-700 p-4 rounded-lg flex justify-between items-center">
                            <div><p class="font-semibold dark:text-white">Sari (Paperlink: Bimbingan Penulisan)</p><p class="text-sm text-slate-500 dark:text-slate-400">26 September 2025, 10:00 WIB</p></div>
                            <a href="#" class="text-sm font-semibold text-sky-600 dark:text-sky-400">Lihat Detail</a>
                        </div>
                    </div>
                </div>
            </div>

            <div id="faqPage" class="page">
                 <h1 class="text-3xl font-bold text-gray-800 dark:text-white mb-6">Pusat Bantuan (FAQ)</h1>
                <div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700 divide-y dark:divide-slate-700">
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Bagaimana cara memesan layanan mentor?</a>
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Apa saja metode pembayaran yang tersedia?</a>
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Bagaimana jika saya tidak puas dengan mentor?</a>
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Apakah saya bisa mengubah jadwal sesi?</a>
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Saya memiliki kendala pada transaksi.</a>
                     <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Bagaimana cara menjadi mentor di EDULINK?</a>
                    <a href="#" onclick="showPage('csChatPage')" class="block py-4 font-semibold cursor-pointer hover:text-sky-500 dark:text-slate-300 dark:hover:text-sky-400">Saya ingin mengajukan keluhan lain.</a>
                </div>
            </div>
            
            <div id="featurePage" class="page p-8">
                 <header class="flex items-center mb-6 max-w-6xl mx-auto"><button onclick="showPage('berandaPage')" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button><h1 id="featureTitle" class="text-3xl font-bold text-gray-800 dark:text-white"></h1></header>
                <div class="w-full max-w-6xl mx-auto">
                    <div id="featureFormContainer" class="bg-white dark:bg-slate-800 p-8 rounded-xl border dark:border-slate-700 shadow-sm"><h2 class="text-2xl font-bold text-blue-800 dark:text-white mb-6 text-center">Cari Mentor Terbaikmu</h2><form id="featureForm" class="space-y-4"></form><button id="searchMentorBtn" class="mt-6 w-full bg-sky-500 text-white font-semibold py-3 px-4 rounded-lg hover:bg-sky-600 transition-transform hover:scale-[1.02]">Cari Mentor</button></div>
                    <div id="mentorResults" class="hidden"><h2 class="text-2xl font-bold text-gray-800 dark:text-white mb-4">Hasil Pencarian Mentor</h2><div id="mentorList" class="space-y-4"></div><button onclick="resetFeaturePage()" class="mt-6 w-full bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-2 px-4 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Cari Lagi</button></div>
                </div>
            </div>

            <div id="paymentPage" class="page"></div>
            
            <div id="promoDetailPage" class="page">
                 <header class="flex items-center mb-6"><button onclick="showPage('promoPage')" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button><h1 class="text-3xl font-bold text-gray-800 dark:text-white">Detail Promo Cashback</h1></header>
                 <div class="bg-white dark:bg-slate-800 p-8 rounded-xl border dark:border-slate-700">
                    <h2 class="text-2xl font-bold text-blue-800 dark:text-sky-400">Dapatkan Cashback 10% dengan E-Wallet!</h2>
                    <p class="text-slate-500 dark:text-slate-400 mt-2 mb-4">Nikmati kemudahan transaksi dan dapatkan keuntungan lebih!</p>
                    <div class="prose max-w-none dark:prose-invert">
                        <p><strong>Periode Promo:</strong> 1 - 30 September 2025</p>
                        <p><strong>Metode Pembayaran:</strong> GoPay, OVO, Dana</p>
                        <h3 class="font-bold mt-4">Syarat dan Ketentuan:</h3>
                        <ul>
                            <li>Promo berlaku untuk semua layanan di EDULINK tanpa minimum transaksi.</li>
                            <li>Maksimal cashback yang didapat adalah Rp 3.000 per transaksi.</li>
                            <li>Setiap pengguna dapat menggunakan promo ini sebanyak 3 kali selama periode promo.</li>
                            <li>Cashback akan diterima maksimal 1x24 jam setelah transaksi berhasil.</li>
                            <li>Promo tidak dapat digabungkan dengan promo lainnya.</li>
                        </ul>
                    </div>
                 </div>
            </div>

            <div id="csChatPage" class="page">
                <header class="flex items-center mb-6"><button onclick="showPage('faqPage')" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button><h1 class="text-3xl font-bold text-gray-800 dark:text-white">Customer Service</h1></header>
                <div class="bg-white dark:bg-slate-800 rounded-xl border dark:border-slate-700 h-[70vh] flex flex-col">
                    <div class="p-4 border-b dark:border-slate-700 flex items-center"><img src="https://placehold.co/40x40/d1fae5/047857?text=CS" class="rounded-full w-10 h-10 mr-3"><div><p class="font-bold dark:text-white">Customer Service</p><p class="text-xs text-green-500">Online</p></div></div>
                    <div id="csChatLog" class="flex-grow p-4 space-y-4 overflow-y-auto"><div class="flex justify-start"><div class="bg-slate-100 dark:bg-slate-700 dark:text-slate-200 p-3 rounded-lg max-w-md">Halo! Ada yang bisa kami bantu? Silakan ketik pertanyaan atau keluhanmu di bawah ini.</div></div></div>
                    <div class="p-4 border-t dark:border-slate-700 flex items-center gap-3"><input id="csChatInput" type="text" placeholder="Ketik pesanmu di sini..." class="w-full px-3 py-2 bg-slate-100 dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-md focus:outline-none focus:ring-sky-500 focus:border-sky-500 dark:text-white"><button id="csSendBtn" class="bg-sky-500 text-white p-2 rounded-md"><i data-lucide="send" class="w-5 h-5"></i></button></div>
                </div>
            </div>
        </main>
    </div>

    <!-- Modals and Notifications -->
    <div id="notification-container" class="fixed top-5 right-5 z-50 space-y-2"></div>
    <div id="shareModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 hidden z-50" onclick="closeShareModal()">
        <div class="modal-content bg-white dark:bg-slate-800 w-full max-w-md rounded-2xl shadow-xl p-6 scale-95 opacity-0" onclick="event.stopPropagation()">
            <h3 class="text-lg font-bold mb-4 dark:text-white">Bagikan Promo Ini!</h3>
            <div class="flex justify-center gap-4 mb-6">
                <a href="#" class="p-3 bg-slate-100 dark:bg-slate-700 rounded-full"><i data-lucide="facebook" class="w-6 h-6 text-blue-600"></i></a>
                <a href="#" class="p-3 bg-slate-100 dark:bg-slate-700 rounded-full"><i data-lucide="twitter" class="w-6 h-6 text-sky-500"></i></a>
                <a href="#" class="p-3 bg-slate-100 dark:bg-slate-700 rounded-full"><i data-lucide="instagram" class="w-6 h-6 text-pink-500"></i></a>
                 <a href="#" class="p-3 bg-slate-100 dark:bg-slate-700 rounded-full"><i data-lucide="message-circle" class="w-6 h-6 text-green-500"></i></a>
            </div>
            <div class="flex items-center">
                <input id="shareLink" type="text" readonly value="https://edulink.app/promo/ajakteman" class="w-full px-3 py-2 bg-slate-100 dark:bg-slate-700 border border-slate-300 dark:border-slate-600 rounded-l-md dark:text-white">
                <button onclick="copyShareLink()" class="bg-sky-500 text-white p-2 rounded-r-md"><i data-lucide="copy" class="w-5 h-5"></i></button>
            </div>
        </div>
    </div>
    <div id="profileModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 hidden z-50" onclick="closeProfileModal()">
        <div class="modal-content bg-white dark:bg-slate-800 w-full max-w-2xl max-h-[90vh] rounded-2xl shadow-xl overflow-hidden flex flex-col scale-95 opacity-0" onclick="event.stopPropagation()">
            <div class="p-4 border-b dark:border-slate-700 flex justify-between items-center bg-slate-50 dark:bg-slate-900"><h2 id="modalProfileTitle" class="text-xl font-bold text-blue-800 dark:text-white">Profil Mentor</h2><button onclick="closeProfileModal()" class="text-slate-400 hover:text-slate-600 p-1 rounded-full"><i data-lucide="x" class="w-6 h-6"></i></button></div>
            <div id="modalProfileBody" class="p-6 overflow-y-auto dark:text-slate-300"></div>
        </div>
    </div>

    <script>
        // --- Data ---
        const universities = ['Universitas Indonesia', 'Universitas Gadjah Mada', 'Universitas Airlangga', 'Institut Teknologi Bandung', 'Universitas Padjadjaran', 'Universitas Brawijaya', 'Universitas Diponegoro', 'IPB University', 'Universitas Sebelas Maret', 'Institut Teknologi Sepuluh Nopember', 'Universitas Hasanuddin', 'Universitas Negeri Malang', 'Universitas Andalas', 'Universitas Negeri Yogyakarta', 'Universitas Negeri Padang', 'Universitas Syiah Kuala', 'Universitas Sumatera Utara', 'Universitas Negeri Semarang', 'Universitas Lampung', 'Universitas Sriwijaya', 'Universitas Riau', 'Universitas Jenderal Soedirman', 'Universitas Udayana', 'Universitas Mataram', 'Universitas Mulawarman', 'Universitas Negeri Surabaya', 'Universitas Negeri Makassar', 'Universitas Jambi', 'Universitas Tanjungpura', 'Universitas Pattimura', 'Universitas Papua', 'Lain-lain'];
        const majors = ['Statistika', 'Ekonomi Pembangunan', 'Fisika', 'Akuntansi', 'Kimia', 'Biologi', 'Manajemen', 'Matematika', 'Farmasi', 'Kedokteran', 'Kedokteran Gigi', 'Kesehatan Masyarakat', 'Ilmu Gizi', 'Keperawatan', 'Psikologi', 'Ilmu Komunikasi', 'Hubungan Internasional', 'Sosiologi', 'Antropologi', 'Ilmu Politik', 'Administrasi Publik', 'Hukum', 'Sastra Indonesia', 'Sastra Inggris', 'Sastra Jepang', 'Pendidikan Bahasa Inggris', 'Pendidikan Matematika', 'Pendidikan Biologi', 'Pendidikan Fisika', 'Pendidikan Kimia', 'Lain-lain'];
        const courseSubjects = ['Kalkulus', 'Statistik', 'Ilmu Ekonomi', 'Akuntansi', 'Fisika', 'Kimia Dasar', 'Biologi Dasar', 'Matematika Lanjut', 'Ekonometrika', 'Pengantar Hukum', 'Pemrograman Dasar', 'Algoritma dan Struktur Data', 'Mikrobiologi', 'Biokimia', 'Farmakologi', 'Anatomi', 'Fisiologi', 'Psikometri', 'Metodologi Penelitian', 'Teori Akuntansi', 'Auditing', 'Manajemen Keuangan', 'Manajemen Operasi', 'Teori Sosiologi', 'Filsafat Ilmu', 'Teori Politik', 'Hubungan Internasional', 'Linguistik Umum', 'Statistika Inferensial', 'Metode Numerik', 'Lain-lain'];
        const consulinkServices = ['Konsultasi Pengerjaan Tugas Akademik', 'Konsultasi Mata Kuliah & Dosen', 'Konsultasi Ujian', 'Konsultasi Kehidupan Kampus'];
        const paperlinkServices = ['Bimbingan Penulisan', 'Bimbingan Metodologi & Analisis Data', 'Review & Proofreading', 'Bimbingan Publikasi'];
        const competitionBranches = ['Business Plan Competition', 'Startup Competition', 'Olimpiade Mahasiswa', 'Data Science Competition', 'Programming Competition', 'Debat Mahasiswa'];
        
        let favoriteMentors = [];

        const mentorData = {
            'Ahmad Maulana': { rating: 4.9, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Kehidupan Kampus', 'Business Plan Competition'], pengalaman: ['- 2 tahun sebagai Konsultan Bisnis Junior'], prestasi: ['- Juara 1 Business Plan Competition Nasional 2023'], keahlian: ['Analisis SWOT', 'Model Bisnis Kanvas'] },
            'Bella Safira': { rating: 4.8, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Kehidupan Kampus', 'Business Plan Competition'], pengalaman: ['- Project Manager di Startup Edukasi'], prestasi: ['- Pemenang Grant Mahasiswa Wirausaha'], keahlian: ['Riset Pasar', 'Public Speaking'] },
            'Candra Wijaya': { rating: 4.7, type: ['courselink', 'paperlink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Statistik', 'Bimbingan Penulisan'], pengalaman: ['- Asisten Riset Dosen'], prestasi: ['- Publikasi di Jurnal Mahasiswa'], keahlian: ['SPSS', 'Penulisan Ilmiah'] },
            'Dian Permata': { rating: 4.9, type: ['courselink', 'paperlink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Ilmu Ekonomi', 'Review & Proofreading'], pengalaman: ['- Tutor Ekonomi Makro'], prestasi: ['- IPK Cum Laude'], keahlian: ['Teori Ekonomi', 'Editing Naskah'] },
            'Eka Saputra': { rating: 4.6, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Ujian', 'Startup Competition'], pengalaman: ['- Co-founder Komunitas Startup Kampus'], prestasi: ['- Finalis kompetisi startup tingkat nasional'], keahlian: ['Pitching', 'Validasi Ide'] },
            'Fina Lestari': { rating: 5.0, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Kehidupan Kampus', 'Business Plan Competition'], pengalaman: ['- Mentor di program orientasi mahasiswa baru'], prestasi: ['- Mahasiswa Berprestasi Tingkat Fakultas'], keahlian: ['Manajemen Waktu', 'Komunikasi Interpersonal'] },
            'Gilang Ramadhan': { rating: 4.8, type: ['courselink', 'paperlink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Akuntansi', 'Bimbingan Metodologi & Analisis Data'], pengalaman: ['- Magang di Divisi Keuangan Perusahaan Multinasional'], prestasi: ['- Sertifikasi Akuntansi Dasar'], keahlian: ['Analisis Laporan Keuangan', 'Riset Kuantitatif'] },
            'Hana Yuliana': { rating: 4.7, type: ['courselink', 'paperlink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Manajemen', 'Bimbingan Publikasi'], pengalaman: ['- Staff Ahli di BEM'], prestasi: ['- Best Paper di Seminar Mahasiswa'], keahlian: ['Manajemen Proyek', 'Sitasi & Referensi'] },
            'Indra Gunawan': { rating: 4.9, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Pengerjaan Tugas Akademik', 'Debat Mahasiswa'], pengalaman: ['- Ketua UKM Debat'], prestasi: ['- Best Speaker di Lomba Debat Regional'], keahlian: ['Argumentasi', 'Riset Cepat'] },
            'Jasmine Putri': { rating: 4.8, type: ['consulink', 'complink'], univ: 'Universitas Indonesia', jurusan: 'Manajemen', spec: 'Pengembangan Karir & Business Plan', services: ['Konsultasi Mata Kuliah & Dosen', 'Olimpiade Mahasiswa'], pengalaman: ['- Asisten Dosen Pengantar Bisnis'], prestasi: ['- Peserta ONMIPA-PT Bidang Ekonomi'], keahlian: ['Problem Solving', 'Teori Manajemen'] },
        };

        const hotServicesData = [
            { type: 'consulink', service: 'Konsultasi Pengerjaan Tugas Akademik', title: 'Konsultasi Tugas Akademik', color: 'emerald'},
            { type: 'consulink', service: 'Konsultasi Ujian', title: 'Konsultasi Persiapan Ujian', color: 'emerald'},
            { type: 'paperlink', service: 'Bimbingan Metodologi & Analisis Data', title: 'Bimbingan Metodologi & Data', color: 'violet'},
            { type: 'courselink', service: 'Kalkulus', title: 'Mentoring Kalkulus', color: 'amber'},
            { type: 'courselink', service: 'Statistik', title: 'Mentoring Statistik', color: 'amber'},
            { type: 'paperlink', service: 'Review & Proofreading', title: 'Jasa Review & Proofreading', color: 'violet'},
            { type: 'paperlink', service: 'Bimbingan Publikasi', title: 'Bimbingan Publikasi Jurnal', color: 'violet'},
            { type: 'complink', service: 'Business Plan Competition', title: 'Mentoring Business Plan', color: 'rose'},
            { type: 'complink', service: 'Programming Competition', title: 'Mentoring Programming Comp.', color: 'rose'},
        ];

        // --- DOM Elements ---
        const authContainer = document.getElementById('authContainer');
        const appWrapper = document.getElementById('app-wrapper');
        const authPages = document.querySelectorAll('.auth-page');
        const pages = document.querySelectorAll('.main-content .page');
        const sidebarLinks = document.querySelectorAll('.sidebar-link');
        const featureForm = document.getElementById('featureForm');
        const featureTitle = document.getElementById('featureTitle');
        const searchMentorBtn = document.getElementById('searchMentorBtn');
        const featureFormContainer = document.getElementById('featureFormContainer');
        const mentorResults = document.getElementById('mentorResults');
        const mentorList = document.getElementById('mentorList');
        const profileModal = document.getElementById('profileModal');
        const modalContent = profileModal.querySelector('.modal-content');
        const modalProfileTitle = document.getElementById('modalProfileTitle');
        const modalProfileBody = document.getElementById('modalProfileBody');

        // --- Functions ---
        function showAuthPage(pageId) { 
            authPages.forEach(p => p.classList.remove('active')); 
            document.getElementById(pageId).classList.add('active'); 
        }
        function login() { 
            authContainer.style.display = 'none';
            appWrapper.classList.remove('hidden'); 
            showPage('berandaPage', document.querySelector('.sidebar-link')); 
        }
        function logout() { 
            appWrapper.classList.add('hidden'); 
            authContainer.style.display = 'block';
            showAuthPage('loginPage'); 
        }
        function showPage(pageId, clickedLink) {
             if (pageId === 'sourcelinkPage') {
                resetSourcelinkPage();
            } else if (pageId === 'favoritPage') {
                updateFavoritesPage();
            }
            pages.forEach(page => page.classList.remove('active')); 
            document.getElementById(pageId).classList.add('active'); 
            if (pageId === 'featurePage') { 
                document.getElementById('app-wrapper').classList.add('feature-view'); 
            } else { 
                document.getElementById('app-wrapper').classList.remove('feature-view'); 
            } 
            sidebarLinks.forEach(link => link.classList.remove('active')); 
            if (pageId === 'featurePage' || pageId === 'promoDetailPage' || pageId === 'csChatPage' || pageId === 'paymentPage') { 
                return; 
            } 
            if (clickedLink) { 
                clickedLink.classList.add('active'); 
            } else { 
                const linkToActivate = Array.from(sidebarLinks).find(link => link.getAttribute('onclick')?.includes(`'${pageId}'`)); 
                if (linkToActivate) { linkToActivate.classList.add('active'); } 
            } 
        }
        function generateOptions(optionsArray, selectedValue = '') { return optionsArray.map(option => `<option value="${option}" ${option === selectedValue ? 'selected' : ''}>${option}</option>`).join(''); }
        function setupFeaturePage(featureType, preselect = {}) {
            featureForm.innerHTML = ''; 
            resetFeaturePage();
            let formContent = '';
            switch (featureType) {
                case 'consulink': featureTitle.textContent = 'Consulink'; formContent = `<div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Universitas</label><select name="univ" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(universities)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Jurusan</label><select name="jurusan" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(majors)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Layanan Konsultasi</label><select name="service" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(consulinkServices, preselect.service)}</select></div>`; break;
                case 'paperlink': featureTitle.textContent = 'Paperlink'; formContent = `<div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Universitas</label><select name="univ" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(universities)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Jurusan</label><select name="jurusan" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(majors)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Layanan Riset & Publikasi</label><select name="service" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(paperlinkServices, preselect.service)}</select></div>`; break;
                case 'courselink': featureTitle.textContent = 'Courselink'; formContent = `<div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Universitas</label><select name="univ" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(universities)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Jurusan</label><select name="jurusan" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(majors)}</select></div><div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Mata Kuliah</label><select name="service" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(courseSubjects, preselect.service)}</select></div>`; break;
                case 'complink': featureTitle.textContent = 'Complink'; formContent = `<div><label class="block text-sm font-medium text-slate-600 dark:text-slate-300">Cabang Lomba Akademik</label><select name="service" class="form-select mt-1 block w-full px-3 py-2 bg-white dark:bg-slate-700 dark:text-white border border-slate-300 dark:border-slate-600 rounded-md shadow-sm">${generateOptions(competitionBranches, preselect.service)}</select></div>`; break;
            }
            featureForm.innerHTML = formContent;
            featureForm.dataset.featureType = featureType;
            showPage('featurePage');
        }
        function openHotService(featureType, serviceName) { setupFeaturePage(featureType, { service: serviceName }); }
        
        function filterAndDisplayMentors() {
            mentorList.innerHTML = '';
            const matchingMentors = Object.entries(mentorData).sort(([,a], [,b]) => b.rating - a.rating);
            if (matchingMentors.length > 0) {
                matchingMentors.forEach(([name, data]) => {
                    let badgeHtml = '';
                    if (data.rating >= 4.9) {
                        badgeHtml = `<div class="absolute top-2 right-2 bg-amber-400 text-white text-xs font-bold px-2 py-1 rounded-full flex items-center gap-1"><i data-lucide="award" class="w-3 h-3"></i> Top Mentor</div>`;
                    } else if (data.rating >= 4.8) {
                         badgeHtml = `<div class="absolute top-2 right-2 bg-sky-500 text-white text-xs font-bold px-2 py-1 rounded-full flex items-center gap-1"><i data-lucide="thumbs-up" class="w-3 h-3"></i> Favorit Mahasiswa</div>`;
                    }
                    const isFavorited = favoriteMentors.includes(name) ? 'favorited' : '';
                    mentorList.innerHTML += `
                        <div class="relative border bg-white dark:bg-slate-800 dark:border-slate-700 rounded-lg p-4 flex items-start space-x-4 hover:bg-slate-50 dark:hover:bg-slate-700/50 transition-colors">
                            ${badgeHtml}
                            <img src="https://placehold.co/64x64/bae6fd/1e3a8a?text=${name.charAt(0)}" class="w-16 h-16 rounded-full flex-shrink-0">
                            <div class="flex-grow">
                                <div class="flex items-center gap-2">
                                    <h4 class="font-bold text-lg text-blue-800 dark:text-white">${name}</h4>
                                     <button onclick="toggleFavorite('${name}', this)" class="favorite-btn ${isFavorited}" title="Tambah ke favorit">
                                        <i data-lucide="heart" class="w-5 h-5 text-slate-400 hover:text-red-500"></i>
                                    </button>
                                </div>
                                <div class="flex items-center gap-1 text-amber-500 mt-1">
                                    <i data-lucide="star" class="w-4 h-4 fill-current"></i>
                                    <span class="font-bold text-sm text-slate-600 dark:text-slate-300">${data.rating.toFixed(1)}</span>
                                </div>
                                <p class="text-sm text-slate-600 dark:text-slate-300 mt-1">${data.univ} - ${data.jurusan}</p>
                                <p class="text-sm text-slate-500 dark:text-slate-400 mt-1">${data.spec}</p>
                            </div>
                            <div class="flex flex-col gap-2 flex-shrink-0 w-40 self-center">
                                <button onclick="openProfileModal('${name}')" class="bg-sky-100 dark:bg-sky-900/50 text-sky-700 dark:text-sky-300 text-sm font-semibold py-2 px-4 rounded-md hover:bg-sky-200 dark:hover:bg-sky-800/50 w-full text-center transition-colors">Lihat Profil</button>
                                <button onclick="showPaymentPage({type: 'Mentor', name: '${name}', price: '6000'})" class="bg-sky-500 text-white text-sm font-semibold py-2 px-4 rounded-md hover:bg-sky-600 w-full text-center transition-colors">Click untuk memilih</button>
                            </div>
                        </div>`;
                });
            } else {
                mentorList.innerHTML = `<div class="text-center py-10 bg-slate-50 dark:bg-slate-800 rounded-lg"><i data-lucide="search-x" class="w-12 h-12 mx-auto text-slate-400"></i><h3 class="mt-4 font-semibold dark:text-white">Mentor tidak ditemukan</h3><p class="text-sm text-slate-500 dark:text-slate-400">Coba ubah kriteria pencarianmu.</p></div>`;
            }
            lucide.createIcons();
        }
        
        function toggleFavorite(mentorName, element) {
            const index = favoriteMentors.indexOf(mentorName);
            if (index > -1) {
                favoriteMentors.splice(index, 1);
                element.classList.remove('favorited');
                showNotification(`${mentorName} dihapus dari favorit.`, 'info');
            } else {
                favoriteMentors.push(mentorName);
                element.classList.add('favorited');
                showNotification(`${mentorName} sedang aktif dan membuka slot baru!`, 'success');
            }
            updateFavoritesPage();
        }
        
        function updateFavoritesPage() {
            const container = document.getElementById('favoriteMentorList');
            container.innerHTML = '';
            if (favoriteMentors.length === 0) {
                 container.innerHTML = `<div class="bg-white dark:bg-slate-800 p-12 rounded-xl border dark:border-slate-700 text-center"><i data-lucide="folder-heart" class="w-16 h-16 mx-auto text-slate-300 dark:text-slate-600 mb-4"></i><h3 class="text-xl font-semibold dark:text-white">Belum Ada Favorit</h3><p class="text-slate-500 dark:text-slate-400 mt-1">Tandai mentor yang kamu sukai untuk akses lebih cepat!</p></div>`;
            } else {
                favoriteMentors.forEach(mentorName => {
                    const data = mentorData[mentorName];
                    if (data) {
                         container.innerHTML += `
                        <div class="border bg-white dark:bg-slate-800 dark:border-slate-700 rounded-lg p-4 flex items-center space-x-4 hover:bg-slate-50 dark:hover:bg-slate-700/50">
                            <img src="https://placehold.co/64x64/bae6fd/1e3a8a?text=${mentorName.charAt(0)}" class="w-16 h-16 rounded-full flex-shrink-0">
                            <div class="flex-grow">
                                <h4 class="font-bold text-lg text-blue-800 dark:text-white">${mentorName}</h4>
                                <p class="text-sm text-slate-600 dark:text-slate-300">${data.univ} - ${data.jurusan}</p>
                                <p class="text-sm text-slate-500 dark:text-slate-400 mt-1">${data.spec}</p>
                            </div>
                            <div class="flex flex-col gap-2 flex-shrink-0 w-40">
                                <button onclick="openProfileModal('${mentorName}')" class="bg-sky-100 dark:bg-sky-900/50 text-sky-700 dark:text-sky-300 text-sm font-semibold py-2 px-4 rounded-md hover:bg-sky-200 dark:hover:bg-sky-800/50 w-full text-center">Lihat Profil</button>
                                <button onclick="showPaymentPage({type: 'Mentor', name: '${mentorName}', price: '6000'})" class="bg-sky-500 text-white text-sm font-semibold py-2 px-4 rounded-md hover:bg-sky-600 w-full text-center">Click untuk memilih</button>
                            </div>
                        </div>`;
                    }
                });
            }
            lucide.createIcons();
        }

        function resetFeaturePage() { featureFormContainer.classList.remove('hidden'); mentorResults.classList.add('hidden'); mentorList.innerHTML = ''; }
        function showNotification(message, type = 'info') { const container = document.getElementById('notification-container'); const notif = document.createElement('div'); const colors = { info: 'bg-blue-500', success: 'bg-green-500', error: 'bg-red-500' }; notif.className = `custom-notification text-white text-sm font-semibold px-4 py-2 rounded-md shadow-lg opacity-0 transform translate-x-10 ${colors[type]}`; notif.textContent = message; container.appendChild(notif); setTimeout(() => { notif.classList.remove('opacity-0', 'translate-x-10'); }, 10); setTimeout(() => { notif.classList.add('opacity-0', 'translate-x-10'); notif.addEventListener('transitionend', () => notif.remove()); }, 3000); }
        function openShareModal() { const modal = document.getElementById('shareModal'); modal.classList.remove('hidden'); setTimeout(() => { modal.classList.remove('opacity-0'); modal.querySelector('.modal-content').classList.remove('scale-95', 'opacity-0'); }, 10); }
        function closeShareModal() { const modal = document.getElementById('shareModal'); modal.querySelector('.modal-content').classList.add('scale-95', 'opacity-0'); modal.classList.add('opacity-0'); setTimeout(() => modal.classList.add('hidden'), 300); }
        function copyShareLink() { navigator.clipboard.writeText('https://edulink.app/promo/ajakteman').then(() => { showNotification('Link disalin!', 'success'); }); }
        
        function openProfileModal(mentorName) {
            const data = mentorData[mentorName];
            if (!data) return;

            modalProfileTitle.textContent = `Profil ${mentorName}`;
            modalProfileBody.innerHTML = `
                <div class="flex flex-col md:flex-row items-start gap-6">
                    <img src="https://placehold.co/128x128/bae6fd/1e3a8a?text=${mentorName.charAt(0)}" class="w-32 h-32 rounded-full mx-auto md:mx-0 flex-shrink-0">
                    <div>
                        <div class="flex items-center gap-4">
                            <h3 class="text-2xl font-bold dark:text-white">${mentorName}</h3>
                            <button onclick="toggleFavorite('${mentorName}', this); this.classList.toggle('favorited')" class="favorite-btn ${favoriteMentors.includes(mentorName) ? 'favorited' : ''}" title="Tambah ke favorit">
                                <i data-lucide="heart" class="w-6 h-6 text-slate-400 hover:text-red-500"></i>
                            </button>
                        </div>
                        <div class="flex items-center gap-1 text-amber-500 mt-2">
                            <i data-lucide="star" class="w-5 h-5 fill-current"></i>
                            <span class="font-bold text-md text-slate-700 dark:text-slate-300">${data.rating.toFixed(1)}</span>
                        </div>
                        <p class="text-md text-slate-600 dark:text-slate-400 mt-2">${data.univ} - ${data.jurusan}</p>
                        <p class="text-md text-sky-600 dark:text-sky-400 font-semibold mt-1">${data.spec}</p>
                    </div>
                </div>
                <div class="mt-6 space-y-4">
                    <div><h4 class="font-bold text-blue-800 dark:text-white border-b dark:border-slate-600 pb-1 mb-2">Pengalaman</h4><ul class="list-disc list-inside text-slate-600 dark:text-slate-400">${data.pengalaman.map(item => `<li>${item}</li>`).join('') || '<li>Data belum tersedia.</li>'}</ul></div>
                    <div><h4 class="font-bold text-blue-800 dark:text-white border-b dark:border-slate-600 pb-1 mb-2">Prestasi</h4><ul class="list-disc list-inside text-slate-600 dark:text-slate-400">${data.prestasi.map(item => `<li>${item}</li>`).join('') || '<li>Data belum tersedia.</li>'}</ul></div>
                    <div><h4 class="font-bold text-blue-800 dark:text-white border-b dark:border-slate-600 pb-1 mb-2">Keahlian</h4><div class="flex flex-wrap gap-2 mt-2">${data.keahlian.map(item => `<span class="bg-sky-100 dark:bg-sky-900/50 text-sky-800 dark:text-sky-300 text-sm font-medium px-3 py-1 rounded-full">${item}</span>`).join('') || '<p class="text-slate-600 dark:text-slate-400">Data belum tersedia.</p>'}</div></div>
                </div>`;
            profileModal.classList.remove('hidden');
            setTimeout(() => { 
                profileModal.classList.remove('opacity-0'); 
                modalContent.classList.remove('scale-95', 'opacity-0'); 
                lucide.createIcons();
            }, 10);
        }

        function closeProfileModal() {
            modalContent.classList.add('scale-95', 'opacity-0');
            profileModal.classList.add('opacity-0');
            setTimeout(() => { profileModal.classList.add('hidden'); }, 300);
        }
        
        function showPaymentPage(item) {
            const paymentContainer = document.getElementById('paymentPage');
            paymentContainer.innerHTML = `
                <header class="flex items-center mb-6"><button onclick="history.back()" class="text-slate-500 dark:text-slate-400 hover:text-sky-500 mr-4 p-2 rounded-full hover:bg-slate-200 dark:hover:bg-slate-700"><i data-lucide="arrow-left" class="w-6 h-6"></i></button><h1 class="text-3xl font-bold text-gray-800 dark:text-white">Konfirmasi Pembayaran</h1></header>
                <div class="max-w-4xl mx-auto">
                    <div id="payment-content" class="bg-white dark:bg-slate-800 rounded-xl border dark:border-slate-700 p-8">
                        <div class="border dark:border-slate-600 rounded-lg p-4 mb-6"><h3 class="font-bold dark:text-white">Detail Pesanan</h3><div class="flex justify-between items-center mt-2 dark:text-slate-300"><span id="transItemName">${item.name}</span><span id="transItemPrice" class="font-bold text-lg dark:text-white">Rp ${Number(item.price).toLocaleString('id-ID')}</span></div></div>
                        <div><h3 class="font-bold mb-4 dark:text-white">Pilih Metode Pembayaran</h3><div class="space-y-3">
                            <label class="flex items-center p-4 border dark:border-slate-600 rounded-lg has-[:checked]:bg-sky-50 dark:has-[:checked]:bg-sky-900/50 has-[:checked]:border-sky-500 dark:has-[:checked]:border-sky-500"><input type="radio" name="payment" class="w-5 h-5 text-sky-600 focus:ring-sky-500 mr-4" checked><span class="font-semibold dark:text-white">E-Wallet (GoPay, OVO, Dana)</span></label>
                            <label class="flex items-center p-4 border dark:border-slate-600 rounded-lg has-[:checked]:bg-sky-50 dark:has-[:checked]:bg-sky-900/50 has-[:checked]:border-sky-500 dark:has-[:checked]:border-sky-500"><input type="radio" name="payment" class="w-5 h-5 text-sky-600 focus:ring-sky-500 mr-4"><span class="font-semibold dark:text-white">Virtual Account (BCA, Mandiri, BRI)</span></label>
                            <label class="flex items-center p-4 border dark:border-slate-600 rounded-lg has-[:checked]:bg-sky-50 dark:has-[:checked]:bg-sky-900/50 has-[:checked]:border-sky-500 dark:has-[:checked]:border-sky-500"><input type="radio" name="payment" class="w-5 h-5 text-sky-600 focus:ring-sky-500 mr-4"><span class="font-semibold dark:text-white">Transfer Bank</span></label>
                            <label class="flex items-center p-4 border dark:border-slate-600 rounded-lg has-[:checked]:bg-sky-50 dark:has-[:checked]:bg-sky-900/50 has-[:checked]:border-sky-500 dark:has-[:checked]:border-sky-500"><input type="radio" name="payment" class="w-5 h-5 text-sky-600 focus:ring-sky-500 mr-4"><span class="font-semibold dark:text-white">Gerai Retail (Alfamart, Indomaret)</span></label>
                            <label class="flex items-center p-4 border dark:border-slate-600 rounded-lg has-[:checked]:bg-sky-50 dark:has-[:checked]:bg-sky-900/50 has-[:checked]:border-sky-500 dark:has-[:checked]:border-sky-500"><input type="radio" name="payment" class="w-5 h-5 text-sky-600 focus:ring-sky-500 mr-4"><span class="font-semibold dark:text-white">Kartu Kredit/Debit</span></label>
                        </div></div>
                        <div class="flex gap-4 mt-8"><button onclick="history.back()" class="w-full bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 font-semibold py-3 rounded-lg hover:bg-slate-300 dark:hover:bg-slate-600">Batal</button><button onclick="processPayment()" class="w-full bg-sky-500 text-white font-semibold py-3 rounded-lg hover:bg-sky-600">Bayar Sekarang</button></div>
                    </div>
                    <div id="payment-processing" class="hidden text-center bg-white dark:bg-slate-800 rounded-xl border dark:border-slate-700 p-8">
                        <div class="w-12 h-12 border-4 border-sky-500 border-t-transparent rounded-full animate-spin mx-auto mb-4"></div>
                        <h2 class="text-xl font-bold dark:text-white">Transaksi sedang diproses...</h2>
                        <p class="text-slate-500 dark:text-slate-400 mt-2">Mohon tunggu sebentar, jangan tutup halaman ini.</p>
                    </div>
                     <div id="payment-reload" class="hidden text-center bg-white dark:bg-slate-800 rounded-xl border dark:border-slate-700 p-8">
                        <i data-lucide="alert-circle" class="w-12 h-12 mx-auto text-amber-500 mb-4"></i><h2 class="text-xl font-bold dark:text-white">Menunggu Konfirmasi</h2><p class="text-slate-500 dark:text-slate-400 mt-2">Jika pembayaran sudah dilakukan, silakan muat ulang status.</p><button onclick="confirmPayment()" class="mt-6 bg-amber-500 text-white font-semibold py-2 px-6 rounded-lg">Muat Ulang</button>
                    </div>
                </div>`;
            lucide.createIcons();
            showPage('paymentPage');
        }
        function processPayment() { document.getElementById('payment-content').classList.add('hidden'); document.getElementById('payment-processing').classList.remove('hidden'); setTimeout(() => { document.getElementById('payment-processing').classList.add('hidden'); document.getElementById('payment-reload').classList.remove('hidden'); }, 3000); }
        function confirmPayment() { showNotification('Pembayaran berhasil!', 'success'); showPage('berandaPage'); }
        function showMentorRegisterForm(category) {
            document.getElementById('mentorRegisterSelection').classList.add('hidden');
            document.getElementById('mentorRegisterFormContainer').classList.remove('hidden');
            document.getElementById('mentorRegisterFormTitle').textContent = `Formulir Pendaftaran Mentor ${category}`;
        }
        function showMentorRegisterSelection() {
            document.getElementById('mentorRegisterSelection').classList.remove('hidden');
            document.getElementById('mentorRegisterFormContainer').classList.add('hidden');
            document.getElementById('mentorRegisterSuccess').classList.add('hidden');
        }
        function submitMentorForm() { 
            document.getElementById('mentorRegisterFormContainer').classList.add('hidden'); 
            document.getElementById('mentorRegisterSuccess').classList.remove('hidden'); 
        }
        function handleCsChat() {
            const input = document.getElementById('csChatInput');
            const chatLog = document.getElementById('csChatLog');
            if (input.value.trim() === '') return;
            chatLog.innerHTML += `<div class="flex justify-end"><div class="bg-blue-800 text-white p-3 rounded-lg max-w-md">${input.value}</div></div>`;
            input.value = '';
            chatLog.scrollTop = chatLog.scrollHeight;
            setTimeout(() => {
                chatLog.innerHTML += `<div class="flex justify-start"><div class="bg-slate-100 dark:bg-slate-700 dark:text-slate-200 p-3 rounded-lg max-w-md">Halo Rifki,<br><br>Terima kasih telah menghubungi EDULINK.<br>Pesan/keluhanmu sudah kami terima dengan baik dan saat ini sedang dalam proses peninjauan oleh tim kami. Mohon bersabar, kami akan segera memberikan balasan maksimal dalam 1x24 jam melalui chat ini atau email yang terdaftar.<br><br>Untuk mempercepat tindak lanjut, pastikan kamu sudah menyertakan informasi yang relevan.<br><br>Jika masalahmu sifatnya darurat, kamu bisa menghubungi kami melalui:<br>📧 support@edulink.com<br>📱 WhatsApp: +62-831-8025-3832</div></div>`;
                chatLog.scrollTop = chatLog.scrollHeight;
            }, 1500);
        }
        function populateHotServices() {
            const container = document.getElementById('hot-services-container');
            let content = `<div class="flex items-center gap-3 mb-5"><i data-lucide="flame" class="w-7 h-7 text-orange-500"></i><h2 class="text-2xl font-bold text-blue-800 dark:text-white">Sedang Ramai Digunakan</h2></div><div class="grid grid-cols-1 md:grid-cols-3 gap-4">`;
            hotServicesData.forEach(item => {
                const userCount = Math.floor(Math.random() * (200 - 20 + 1)) + 20;
                content += `<div onclick="openHotService('${item.type}', '${item.service}')" class="bg-slate-100 dark:bg-slate-700/50 p-4 rounded-lg cursor-pointer hover:bg-slate-200/70 dark:hover:bg-slate-700">
                                <div class="flex justify-between items-start">
                                    <div><h4 class="font-semibold dark:text-white">${item.title}</h4><p class="text-sm text-${item.color}-600 dark:text-${item.color}-400 font-medium capitalize">${item.type}</p></div>
                                    <i data-lucide="arrow-right" class="w-5 h-5 text-slate-400 dark:text-slate-500 flex-shrink-0"></i>
                                </div>
                                <p class="text-xs text-slate-500 dark:text-slate-400 mt-2">${userCount} orang sedang menggunakan</p>
                            </div>`;
            });
            content += `</div>`;
            container.innerHTML = content;
        }

        function populateTestimonials() {
            const container = document.getElementById('testimonials-container');
            let content = `<div class="flex items-center gap-3 mb-5"><i data-lucide="quote" class="w-7 h-7 text-green-500"></i><h2 class="text-2xl font-bold text-blue-800 dark:text-white">Kisah Sukses</h2></div><div class="grid grid-cols-1 md:grid-cols-2 gap-6">`;
            const testimonials = [
                { name: 'Rina S.', achievement: 'Lolos Publikasi Jurnal Scopus Q2', quote: 'Mentor Paperlink sangat membantu dalam menyusun naskah dan memilih jurnal. Prosesnya jadi jauh lebih cepat dan terarah!', photo: 'https://placehold.co/80x80/c7d2fe/4338ca?text=RS' },
                { name: 'Adi P.', achievement: 'Juara 1 Business Plan Competition', quote: 'Dapat bimbingan dari mentor Complink yang berpengalaman membuat business plan saya jadi lebih matang dan menarik di mata juri.', photo: 'https://placehold.co/80x80/bbf7d0/166534?text=AP' }
            ];
            testimonials.forEach(item => {
                content += `<div class="bg-white dark:bg-slate-800 p-6 rounded-xl border dark:border-slate-700 flex gap-5 items-start">
                                <div class="w-20 h-20 rounded-full bg-slate-200 flex-shrink-0" style="background-image:url(${item.photo}); background-size:cover;"></div>
                                <div>
                                    <p class="text-slate-600 dark:text-slate-300 italic">"${item.quote}"</p>
                                    <p class="font-bold text-slate-800 dark:text-white mt-3">${item.name}</p>
                                    <p class="text-sm text-green-600 dark:text-green-400 font-semibold">${item.achievement}</p>
                                </div>
                           </div>`;
            });
            content += `</div>`;
            container.innerHTML = content;
        }


        function showSourcelinkStep2() {
            document.getElementById('sourcelinkStep1').classList.add('hidden');
            document.getElementById('sourcelinkStep2').classList.remove('hidden');
        }
        function submitSourcelink() {
            document.getElementById('sourcelinkStep2').classList.add('hidden');
            document.getElementById('sourcelinkSuccess').classList.remove('hidden');
        }
        function resetSourcelinkPage() {
            document.getElementById('sourcelinkStep1').classList.remove('hidden');
            document.getElementById('sourcelinkStep2').classList.add('hidden');
            document.getElementById('sourcelinkSuccess').classList.add('hidden');
            if(document.getElementById('sourcelinkCriteriaForm')) {
                 document.getElementById('sourcelinkCriteriaForm').reset();
            }
            if(document.getElementById('sourcelinkLinkForm')) {
                document.getElementById('sourcelinkLinkForm').reset();
            }
        }
        
        // Dark/Light Mode Toggle
        const themeToggleBtn = document.getElementById('theme-toggle');
        const themeToggleDarkIcon = document.getElementById('theme-toggle-dark-icon');
        const themeToggleLightIcon = document.getElementById('theme-toggle-light-icon');

        if (localStorage.getItem('color-theme') === 'dark' || (!('color-theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            themeToggleLightIcon.classList.remove('hidden');
            document.documentElement.classList.add('dark');
        } else {
            themeToggleDarkIcon.classList.remove('hidden');
            document.documentElement.classList.remove('dark');
        }

        themeToggleBtn.addEventListener('click', function() {
            themeToggleDarkIcon.classList.toggle('hidden');
            themeToggleLightIcon.classList.toggle('hidden');
            if (localStorage.getItem('color-theme')) {
                if (localStorage.getItem('color-theme') === 'light') {
                    document.documentElement.classList.add('dark');
                    localStorage.setItem('color-theme', 'dark');
                } else {
                    document.documentElement.classList.remove('dark');
                    localStorage.setItem('color-theme', 'light');
                }
            } else {
                if (document.documentElement.classList.contains('dark')) {
                    document.documentElement.classList.remove('dark');
                    localStorage.setItem('color-theme', 'light');
                } else {
                    document.documentElement.classList.add('dark');
                    localStorage.setItem('color-theme', 'dark');
                }
            }
        });


        document.addEventListener('DOMContentLoaded', () => { 
            populateHotServices();
            populateTestimonials();
            lucide.createIcons();
            searchMentorBtn.addEventListener('click', () => { if (!featureForm.checkValidity()) { featureForm.reportValidity(); return; } featureFormContainer.classList.add('hidden'); mentorResults.classList.remove('hidden'); filterAndDisplayMentors(); });
            document.getElementById('csSendBtn').addEventListener('click', handleCsChat);
            document.getElementById('csChatInput').addEventListener('keypress', (e) => { if (e.key === 'Enter') handleCsChat(); });

            // Make the script executable by attaching functions to window
            window.showAuthPage = showAuthPage;
            window.login = login;
            window.logout = logout;
            window.showPage = showPage;
            window.setupFeaturePage = setupFeaturePage;
            window.openHotService = openHotService;
            window.filterAndDisplayMentors = filterAndDisplayMentors;
            window.resetFeaturePage = resetFeaturePage;
            window.showNotification = showNotification;
            window.openShareModal = openShareModal;
            window.closeShareModal = closeShareModal;
            window.copyShareLink = copyShareLink;
            window.openProfileModal = openProfileModal;
            window.closeProfileModal = closeProfileModal;
            window.showPaymentPage = showPaymentPage;
            window.processPayment = processPayment;
            window.confirmPayment = confirmPayment;
            window.submitMentorForm = submitMentorForm;
            window.handleCsChat = handleCsChat;
            window.showMentorRegisterForm = showMentorRegisterForm;
            window.showMentorRegisterSelection = showMentorRegisterSelection;
            window.showSourcelinkStep2 = showSourcelinkStep2;
            window.submitSourcelink = submitSourcelink;
            window.resetSourcelinkPage = resetSourcelinkPage;
            window.toggleFavorite = toggleFavorite;
        });
    </script>
</body>
</html>

