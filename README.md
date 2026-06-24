<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Manajemen Kelas Terpadu VII G - MTsN 2 Jember</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; font-family: 'Poppins', sans-serif; margin: 0; padding: 0; }
        body { background-color: #f4f6f9; color: #333; display: flex; min-height: 100vh; flex-direction: column; }
        
        /* HALAMAN LOGIN */
        .login-container { display: flex; align-items: center; justify-content: center; min-height: 100vh; background: linear-gradient(135deg, #113f2a 0%, #1a5238 100%); padding: 20px; }
        .login-card { background: white; padding: 35px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.2); width: 100%; max-width: 400px; text-align: center; }
        .login-card h2 { color: #113f2a; margin-bottom: 5px; font-size: 24px; font-weight: 700; }
        .login-card h3 { color: #d4af37; margin-bottom: 25px; font-size: 14px; font-weight: 500; letter-spacing: 1px; }
        .form-group { margin-bottom: 18px; text-align: left; }
        .form-group label { display: block; font-size: 13px; margin-bottom: 6px; color: #555; font-weight: 500; }
        .form-control { width: 100%; padding: 10px 14px; border: 1px solid #ccc; border-radius: 6px; font-size: 14px; transition: 0.2s; }
        .form-control:focus { border-color: #113f2a; outline: none; box-shadow: 0 0 0 3px rgba(17,63,42,0.1); }
        .btn-login { width: 100%; padding: 12px; background: #113f2a; color: white; border: none; border-radius: 6px; font-size: 14px; font-weight: 600; cursor: pointer; transition: 0.2s; margin-top: 10px; }
        .btn-login:hover { background: #1a5238; }

        /* APP LAYOUT */
        .app-wrapper { display: none; min-height: 100vh; width: 100%; }
        .sidebar { width: 280px; background-color: #113f2a; color: white; padding: 20px 0; display: flex; flex-direction: column; flex-shrink: 0; }
        .sidebar-brand { text-align: center; padding: 10px 20px 20px 20px; border-bottom: 1px solid rgba(255,255,255,0.1); }
        .sidebar-brand h2 { font-size: 20px; font-weight: 700; color: #d4af37; }
        .sidebar-menu { list-style: none; margin-top: 15px; overflow-y: auto; flex: 1; }
        .sidebar-menu li { padding: 12px 20px; cursor: pointer; display: flex; align-items: center; gap: 10px; transition: 0.2s; font-size: 13.5px; }
        .sidebar-menu li:hover, .sidebar-menu li.active { background-color: #1a5238; border-left: 4px solid #d4af37; }
        
        .main-content { flex: 1; padding: 25px; display: flex; flex-direction: column; overflow-y: auto; background-color: #f4f6f9; }
        .header-content { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; border-bottom: 2px solid #e0e0e0; padding-bottom: 10px; flex-wrap: wrap; gap: 10px; }
        .header-content h1 { font-size: 22px; color: #113f2a; }
        
        /* DASHBOARD GRID */
        .dashboard-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px; margin-top: 10px; }
        .card-menu { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); text-align: center; cursor: pointer; transition: 0.3s; border-top: 4px solid #113f2a; }
        .card-menu:hover { transform: translateY(-3px); box-shadow: 0 6px 12px rgba(0,0,0,0.1); }
        .card-menu h3 { font-size: 16px; margin-bottom: 6px; color: #113f2a; }
        .card-menu p { font-size: 12px; color: #666; }

        /* ACTION BAR & BUTTONS */
        .action-bar { background: white; padding: 12px 20px; border-radius: 8px; margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 4px rgba(0,0,0,0.02); flex-wrap: wrap; gap: 10px; }
        .btn { padding: 8px 14px; font-size: 12.5px; font-weight: 600; border: none; border-radius: 5px; cursor: pointer; display: inline-flex; align-items: center; gap: 8px; transition: 0.2s; }
        .btn-download { background-color: #b08218; color: white; }
        .btn-download:hover { background-color: #d4af37; }
        .btn-add { background-color: #0288d1; color: white; }
        .btn-add:hover { background-color: #039be5; }
        .btn-edit { background-color: #ffa000; color: white; padding: 4px 8px; font-size: 11px; }
        .btn-delete { background-color: #d32f2f; color: white; padding: 4px 8px; font-size: 11px; }
        .btn-logout { background-color: #b01212; color: white; padding: 6px 12px; font-size: 12px; }
        .btn-logout:hover { background-color: #d32f2f; }
        .btn-upload-label { background-color: #113f2a; color: white; padding: 8px 14px; font-size: 12.5px; font-weight: 600; border-radius: 5px; cursor: pointer; display: inline-flex; align-items: center; gap: 8px; transition: 0.2s; }
        .btn-upload-label:hover { background-color: #1a5238; }
        .file-input { display: none; }

        /* TABLES */
        .table-responsive { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); overflow-x: auto; }
        table { width: 100%; border-collapse: collapse; text-align: left; font-size: 13.5px; min-width: 600px; }
        th, td { padding: 12px 12px; border-bottom: 1px solid #eee; }
        th { background-color: #f8f9fa; color: #113f2a; font-weight: 600; }
        tr:hover { background-color: #fdfdfd; }
        .action-cells { display: flex; gap: 5px; }
        .page-section { display: none; }
        .page-section.active { display: block; }
        .file-badge { background-color: #e8f5e9; color: #2e7d32; padding: 3px 8px; border-radius: 4px; font-size: 11.5px; font-weight: 500; display: inline-block; word-break: break-all; }
        
        @media (max-width: 768px) {
            body { flex-direction: column; }
            .app-wrapper { flex-direction: column; }
            .sidebar { width: 100%; }
            .sidebar-brand { padding: 15px; }
            .sidebar-menu { display: flex; flex-wrap: wrap; max-height: 180px; }
            .sidebar-menu li { flex: 1 1 45%; padding: 8px 12px; font-size: 12px; }
            .main-content { padding: 15px; }
        }
    </style>
</head>
<body>

    <!-- ==================== HALAMAN LOGIN ==================== -->
    <div class="login-container" id="login-page">
        <div class="login-card">
            <h2>MTsN 2 JEMBER</h2>
            <h3>SIAKAD VII G</h3>
            <div class="form-group">
                <label>Pilih Akses Masuk</label>
                <select class="form-control" id="login-role" onchange="toggleLoginFields()">
                    <option value="guru">Wali Kelas / Guru</option>
                    <option value="siswa">Siswa Kelas VII G</option>
                </select>
            </div>
            <div id="extra-login-fields" style="display: none;">
                <div class="form-group">
                    <label>Pilih Kelas</label>
                    <select class="form-control" id="login-kelas">
                        <option value="VII G">Kelas VII G</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Nomor Absen Siswa</label>
                    <input type="number" class="form-control" id="login-absen" placeholder="Contoh: 1, 2, 3..." min="1">
                </div>
            </div>
            <div class="form-group">
                <label>Kata Sandi / PIN</label>
                <input type="password" class="form-control" id="login-password" placeholder="Masukkan PIN pengenal">
            </div>
            <button class="btn-login" onclick="handleLogin()">Masuk ke Aplikasi</button>
        </div>
    </div>

    <!-- ==================== HALAMAN UTAMA APLIKASI ==================== -->
    <div class="app-wrapper" id="app-dashboard">
        <!-- SIDEBAR -->
        <div class="sidebar">
            <div class="sidebar-brand">
                <h2>MTsN 2 JEMBER</h2>
                <p style="font-size: 11px; color: #a5d6a7;" id="user-display-role">Aplikasi Kelas VII G</p>
            </div>
            <ul class="sidebar-menu">
                <li class="active" id="nav-menu-utama" onclick="switchPage('menu-utama')">🏠 Menu Utama</li>
                <li id="nav-data-siswa" onclick="switchPage('data-siswa')">👥 Data Siswa</li>
                <li id="nav-absen-siswa" onclick="switchPage('absen-siswa')">📅 Absen Siswa</li>
                <li id="nav-nilai-siswa" onclick="switchPage('nilai-siswa')">📝 Nilai Siswa</li>
                <li id="nav-bank-soal" onclick="switchPage('bank-soal')">🗂️ Bank Soal</li>
                <li id="nav-jurnal-catatan" onclick="switchPage('jurnal-catatan')">📔 Jurnal Guru</li>
                <li id="nav-perangkat-ajar" onclick="switchPage('perangkat-ajar')">🛠️ Perangkat Ajar</li>
                <li id="nav-modul-ajar" onclick="switchPage('modul-ajar')">📖 Modul Ajar</li>
                <li id="nav-jadwal-pelajaran" onclick="switchPage('jadwal-pelajaran')">📚 Jadwal Pelajaran</li>
                <li id="nav-jadwal-piket" onclick="switchPage('jadwal-piket')">🧹 Jadwal Piket</li>
            </ul>
        </div>

        <!-- KONTEN -->
        <div class="main-content">
            <div class="header-content">
                <h1 id="page-title">Menu Utama</h1>
                <div style="display: flex; align-items: center; gap: 15px;">
                    <div style="font-size: 13px; font-weight: 500; color: #666;" id="identity-banner">Wali Kelas: <b>Hariyanto, S.Pd.I</b></div>
                    <button class="btn btn-logout" onclick="handleLogout()">🚪 Keluar</button>
                </div>
            </div>

            <!-- MENU UTAMA -->
            <div id="menu-utama" class="page-section active">
                <p style="margin-bottom: 15px; color: #666;">Selamat datang di Pusat Kontrol Administrasi Integrasi Jaringan Lokal Madrasah.</p>
                <div class="dashboard-grid">
                    <div class="card-menu" onclick="switchPage('data-siswa')"><h3>👥 Data Siswa</h3><p>Profil & NISN siswa</p></div>
                    <div class="card-menu" onclick="switchPage('absen-siswa')"><h3>📅 Absen Siswa</h3><p>Rekap kehadiran harian</p></div>
                    <div class="card-menu" onclick="switchPage('nilai-siswa')"><h3>📝 Nilai Siswa</h3><p>Input Nilai Komponen</p></div>
                    <div class="card-menu" onclick="switchPage('bank-soal')"><h3>🗂️ Bank Soal</h3><p>Manajemen file uji dokumen</p></div>
                    <div class="card-menu" onclick="switchPage('jurnal-catatan')"><h3>📔 Jurnal Guru</h3><p>Catatan mengajar harian</p></div>
                    <div class="card-menu" onclick="switchPage('perangkat-ajar')"><h3>🛠️ Perangkat Ajar</h3><p>Administrasi Silabus & RPP</p></div>
                    <div class="card-menu" onclick="switchPage('modul-ajar')"><h3>📖 Modul Ajar</h3><p>Bahan ajar & modul KBC</p></div>
                    <div class="card-menu" onclick="switchPage('jadwal-pelajaran')"><h3>📚 Jadwal Pelajaran</h3><p>Jam belajar mingguan</p></div>
                    <div class="card-menu" onclick="switchPage('jadwal-piket')"><h3>🧹 Jadwal Piket</h3><p>Kebersihan ruang kelas</p></div>
                </div>
            </div>

            <!-- DATA SISWA -->
            <div id="data-siswa" class="page-section">
                <div class="action-bar">
                    <div id="admin-student-actions">
                        <label class="btn-upload-label" style="margin-right: 5px;">📤 Upload CSV Siswa
                            <input type="file" class="file-input" accept=".csv" onchange="handleMasterStudentUpload(this)">
                        </label>
                        <button class="btn btn-add" onclick="addNewStudentPrompt()">➕ Tambah Siswa</button>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-siswa', 'Data_Siswa_7G')">📥 Unduh CSV</button>
                </div>
                <div class="table-responsive">
                    <table id="table-siswa">
                        <thead><tr><th>No</th><th>NISN</th><th>Nama Siswa</th><th>Jenis Kelamin</th><th>Status</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- ABSEN SISWA -->
            <div id="absen-siswa" class="page-section">
                <div class="action-bar">
                    <span style="font-size: 13px; color: #666;">Rekapitulasi kehadiran periodik komparatif siswa VII G.</span>
                    <button class="btn btn-download" onclick="downloadData('table-absen', 'Rekap_Absen_7G')">📥 Unduh Rekap</button>
                </div>
                <div class="table-responsive">
                    <table id="table-absen">
                        <thead><tr><th>No</th><th>Nama Siswa</th><th>Hadir</th><th>Sakit</th><th>Izin</th><th>Alfa</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- NILAI SISWA -->
            <div id="nilai-siswa" class="page-section">
                <div class="action-bar">
                    <span style="font-size: 13px; color: #666;">Daftar komponen perolehan nilai rerata terpadu.</span>
                    <button class="btn btn-download" onclick="downloadData('table-nilai', 'Data_Nilai_7G')">📥 Unduh Buku Nilai</button>
                </div>
                <div class="table-responsive">
                    <table id="table-nilai">
                        <thead><tr><th>No</th><th>Nama Siswa</th><th>Nilai Harian</th><th>Nilai Tugas</th><th>Nilai Praktek</th><th>Rata-rata</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

            <!-- BANK SOAL -->
            <div id="bank-soal" class="page-section">
                <div class="action-bar">
                    <div class="admin-only-action">
                        <label class="btn-upload-label">📁 Upload Dokumen Soal (Word/PDF/Excel)
                            <input type="file" class="file-input" accept=".docx, .doc, .pdf, .xlsx, .xls" onchange="handleAdminDocumentUpload(this, 'bank-soal')">
                        </label>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-soal', 'Bank_Soal_7G')">📥 Unduh Daftar</button>
                </div>
                <div class="table-responsive">
                    <table id="table-soal">
                        <thead><tr><th>No</th><th>Nama Dokumen / File Soal</th><th>Mata Pelajaran</th><th>Tanggal Unggah</th><th>Ukuran File</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody>
                            <tr><td>1</td><td><span class="file-badge">Soal_Quran_Hadits_Bab_Mad.docx</span></td><td>Al-Qur'an Hadits</td><td>15 Juni 2026</td><td>24 KB</td><td class="action-column"><button class="btn btn-delete" onclick="this.closest('tr').remove(); reorderTableIndex('table-soal');">🗑️ Hapus</button></td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- JURNAL -->
            <div id="jurnal-catatan" class="page-section">
                <div class="action-bar">
                    <div class="admin-only-action">
                        <label class="btn-upload-label">📤 Upload Jurnal CSV
                            <input type="file" class="file-input" accept=".csv" onchange="uploadGenericTable(this, 'table-jurnal')">
                        </label>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-jurnal', 'Jurnal_Mengajar_7G')">📥 Unduh Jurnal</button>
                </div>
                <div class="table-responsive">
                    <table id="table-jurnal">
                        <thead><tr><th>Tanggal / Hari</th><th>Mata Pelajaran</th><th>Materi Pembelajaran</th><th>Hambatan Catatan</th><th>Tindak Lanjut</th></tr></thead>
                        <tbody>
                            <tr><td>15 Juni 2026</td><td>Al-Qur'an Hadits</td><td>Evaluasi Tajwid Surah Pendek</td><td>3 anak belum lancar makhraj</td><td>Bimbingan personal jam istirahat</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- PERANGKAT AJAR -->
            <div id="perangkat-ajar" class="page-section">
                <div class="action-bar">
                    <div class="admin-only-action">
                        <label class="btn-upload-label">📁 Upload Perangkat (Word/PDF/Excel)
                            <input type="file" class="file-input" accept=".docx, .doc, .pdf, .xlsx, .xls" onchange="handleAdminDocumentUpload(this, 'perangkat-ajar')">
                        </label>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-perangkat', 'Perangkat_Ajar_7G')">📥 Unduh Daftar</button>
                </div>
                <div class="table-responsive">
                    <table id="table-perangkat">
                        <thead><tr><th>No</th><th>Nama Dokumen Perangkat</th><th>Mata Pelajaran</th><th>Tanggal Unggah</th><th>Ukuran File</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody>
                            <tr><td>1</td><td><span class="file-badge">ATP_Akidah_Akhlak_7.pdf</span></td><td>Akidah Akhlak</td><td>16 Juni 2026</td><td>1.2 MB</td><td class="action-column"><button class="btn btn-delete" onclick="this.closest('tr').remove(); reorderTableIndex('table-perangkat');">🗑️ Hapus</button></td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- MODUL AJAR -->
            <div id="modul-ajar" class="page-section">
                <div class="action-bar">
                    <div class="admin-only-action">
                        <label class="btn-upload-label">📁 Upload Modul Ajar (Word/PDF/Excel)
                            <input type="file" class="file-input" accept=".docx, .doc, .pdf, .xlsx, .xls" onchange="handleAdminDocumentUpload(this, 'modul-ajar')">
                        </label>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-modul', 'Modul_Ajar_7G')">📥 Unduh Daftar</button>
                </div>
                <div class="table-responsive">
                    <table id="table-modul">
                        <thead><tr><th>No</th><th>Nama Dokumen Modul</th><th>Mata Pelajaran</th><th>Tanggal Unggah</th><th>Ukuran File</th><th class="action-column">Aksi</th></tr></thead>
                        <tbody>
                            <tr><td>1</td><td><span class="file-badge">Modul_KBC_Karakter_VII.docx</span></td><td>Kurikulum Berbasis Cinta</td><td>18 Juni 2026</td><td>450 KB</td><td class="action-column"><button class="btn btn-delete" onclick="this.closest('tr').remove(); reorderTableIndex('table-modul');">🗑️ Hapus</button></td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- JADWAL -->
            <div id="jadwal-pelajaran" class="page-section">
                <div class="action-bar">
                    <div class="admin-only-action">
                        <label class="btn-upload-label">📤 Upload Jadwal CSV
                            <input type="file" class="file-input" accept=".csv" onchange="uploadGenericTable(this, 'table-jadwal')">
                        </label>
                    </div>
                    <button class="btn btn-download" onclick="downloadData('table-jadwal', 'Jadwal_Pelajaran_7G')">📥 Unduh Jadwal</button>
                </div>
                <div class="table-responsive">
                    <table id="table-jadwal">
                        <thead><tr><th>Hari</th><th>Jam Ke-1 & 2</th><th>Jam Ke-3 & 4</th><th>Jam Ke-5 & 6</th><th>Jam Ke-7 & 8</th></tr></thead>
                        <tbody>
                            <tr><td>Senin</td><td>Al-Qur'an Hadits</td><td>Matematika</td><td>Bahasa Indonesia</td><td>Fiqih</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- PIKET -->
            <div id="jadwal-piket" class="page-section">
                <div class="action-bar">
                    <span style="font-size: 13px; color: #666;">Pembagian tim kerja kebersihan harian ruang kelas.</span>
                    <button class="btn btn-download" onclick="downloadData('table-piket', 'Jadwal_Piket_7G')">📥 Unduh Tim Piket</button>
                </div>
                <div class="table-responsive">
                    <table id="table-piket">
                        <thead><tr><th>Hari</th><th>Anggota Anggota Piket Kebersihan</th></tr></thead>
                        <tbody></tbody>
                    </table>
                </div>
            </div>

        </div>
    </div>

    <!-- SCRIPT UTAMA KONTROL SISTEM -->
    <script>
        let currentRole = "guru";
        let globalStudents = [
            { id: 1, nisn: "3123362667", nama: "KEISHA ANNAFI ZAHRA", jk: "Perempuan", status: "Aktif" },
            { id: 2, nisn: "0129845056", nama: "AZZAMY SYAUQI GHEAZ", jk: "Laki-laki", status: "Aktif" }
        ];
        let globalGrades = {
            1: { harian: 85, tugas: 85, praktek: 85 },
            2: { harian: 80, tugas: 85, praktek: 90 }
        };
        let globalAttendance = {
            1: { hadir: 24, sakit: 0, izin: 0, alfa: 0 },
            2: { hadir: 23, sakit: 1, izin: 0, alfa: 0 }
        };

        document.addEventListener("DOMContentLoaded", () => {
            syncAllPanels();
        });

        function toggleLoginFields() {
            const role = document.getElementById("login-role").value;
            const extraFields = document.getElementById("extra-login-fields");
            extraFields.style.display = (role === "siswa") ? "block" : "none";
        }

        function handleLogin() {
            const role = document.getElementById("login-role").value;
            const password = document.getElementById("login-password").value;
            
            if (role === "guru") {
                if (password !== "1234") {
                    alert("PIN Wali Kelas Salah!");
                    return;
                }
                currentRole = "guru";
                document.getElementById("identity-banner").innerHTML = "Wali Kelas: <b>Hariyanto, S.Pd.I</b>";
                document.getElementById("user-display-role").innerText = "Akses: Wali Kelas (Full)";
                setAdminVisibility(true);
            } else {
                const classSelect = document.getElementById("login-kelas").value;
                const absNum = document.getElementById("login-absen").value;
                if (!absNum || password !== "5678") {
                    alert("Nomor Absen atau PIN Siswa Salah!");
                    return;
                }
                currentRole = "siswa";
                document.getElementById("identity-banner").innerHTML = `Siswa Absen: <b>${absNum} (${classSelect})</b>`;
                document.getElementById("user-display-role").innerText = `Akses: Siswa (Lihat Data)`;
                setAdminVisibility(false);
            }

            document.getElementById("login-page").style.display = "none";
            document.getElementById("app-dashboard").style.display = "flex";
            switchPage('menu-utama');
        }

        function handleLogout() {
            document.getElementById("login-password").value = "";
            document.getElementById("login-absen").value = "";
            document.getElementById("app-dashboard").style.display = "none";
            document.getElementById("login-page").style.display = "flex";
        }

        function setAdminVisibility(isAdmin) {
            const displayValue = isAdmin ? "inline-flex" : "none";
            document.getElementById("admin-student-actions").style.display = displayValue;
            document.querySelectorAll(".admin-only-action").forEach(el => el.style.display = displayValue);
            document.querySelectorAll(".action-column").forEach(el => el.style.display = isAdmin ? "table-cell" : "none");
        }

        function switchPage(pageId) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.sidebar-menu li').forEach(li => li.classList.remove('active'));
            
            document.getElementById(pageId).classList.add('active');
            const navElement = document.getElementById('nav-' + pageId);
            if (navElement) navElement.classList.add('active');
            
            const titles = {
                'menu-utama': '🏠 Menu Utama / Dashboard',
                'data-siswa': '👥 Administrasi Data Siswa',
                'absen-siswa': '📅 Rekap Kehadiran (Absensi) Siswa',
                'nilai-siswa': '📝 Buku Komponen Nilai Siswa',
                'bank-soal': '🗂️ Bank Evaluasi Soal',
                'jurnal-catatan': '📔 Jurnal Mengajar & Catatan Guru',
                'perangkat-ajar': '🛠️ Perangkat Ajar Kurikulum',
                'modul-ajar': '📖 Bank Modul Ajar Tematik',
                'jadwal-pelajaran': '📚 Jadwal Pelajaran Mingguan',
                'jadwal-piket': '🧹 Jadwal Piket Kebersihan Kelas'
            };
            document.getElementById('page-title').innerText = titles[pageId] || 'Aplikasi Wali Kelas';
        }

        function handleAdminDocumentUpload(input, panelType) {
            const file = input.files[0];
            if (!file) return;

            const mapel = prompt("Masukkan Mata Pelajaran untuk berkas ini:", "Al-Qur'an Hadits");
            if (mapel === null) return;

            let targetTableId = (panelType === "bank-soal") ? "table-soal" : (panelType === "perangkat-ajar" ? "table-perangkat" : "table-modul");
            const tbody = document.getElementById(targetTableId).querySelector("tbody");

            let sizeStr = (file.size / 1024).toFixed(0) + " KB";
            if (file.size > 1024 * 1024) sizeStr = (file.size / (1024 * 1024)).toFixed(1) + " MB";

            const hariIni = new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'long', year: 'numeric' });
            const nextNo = tbody.rows.length + 1;

            const newRow = document.createElement("tr");
            newRow.innerHTML = `
                <td>${nextNo}</td>
                <td><span class="file-badge">${file.name}</span></td>
                <td>${mapel}</td>
                <td>${hariIni}</td>
                <td>${sizeStr}</td>
                <td class="action-column"><button class="btn btn-delete" onclick="this.closest('tr').remove(); reorderTableIndex('${targetTableId}');">🗑️ Hapus</button></td>
            `;
            tbody.appendChild(newRow);
            setAdminVisibility(currentRole === "guru");
            input.value = '';
        }

        function reorderTableIndex(tableId) {
            const tbody = document.getElementById(tableId).querySelector("tbody");
            Array.from(tbody.rows).forEach((row, idx) => { row.cells[0].innerText = idx + 1; });
        }

        function handleMasterStudentUpload(input) {
            const file = input.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                const text = e.target.result;
                const lines = text.split(/\r?\n/);
                if(lines.length <= 1) return;

                globalStudents = [];
                let studentId = 1;
                for (let i = 1; i < lines.length; i++) {
                    if (lines[i].trim() === "") continue;
                    const cols = lines[i].split(/[,;](?=(?:(?:[^"]*"){2})*[^"]*$)/);
                    if(cols.length >= 3) {
                        globalStudents.push({
                            id: studentId,
                            nisn: cols[1] ? cols[1].replace(/"/g, "").trim() : "-",
                            nama: cols[2] ? cols[2].replace(/"/g, "").trim().toUpperCase() : "-",
                            jk: cols[3] ? cols[3].replace(/"/g, "").trim() : "Laki-laki",
                            status: cols[4] ? cols[4].replace(/"/g, "").trim() : "Aktif"
                        });
                        if (!globalGrades[studentId]) globalGrades[studentId] = { harian: 0, tugas: 0, praktek: 0 };
                        if (!globalAttendance[studentId]) globalAttendance[studentId] = { hadir: 0, sakit: 0, izin: 0, alfa: 0 };
                        studentId++;
                    }
                }
                syncAllPanels();
                alert("Master data siswa berhasil disinkronkan.");
            };
            reader.readAsText(file);
            input.value = '';
        }

        function addNewStudentPrompt() {
            const nisn = prompt("Masukkan NISN:"); if (nisn === null) return;
            const nama = prompt("Masukkan Nama Siswa:"); if (!nama) return;
            const jk = prompt("Jenis Kelamin (Laki-laki/Perempuan):", "Laki-laki");
            const status = prompt("Status (Aktif/Mutasi):", "Aktif");

            const nextId = globalStudents.length > 0 ? Math.max(...globalStudents.map(s => s.id)) + 1 : 1;
            globalStudents.push({ id: nextId, nisn: nisn, nama: nama.toUpperCase(), jk: jk, status: status });
            globalGrades[nextId] = { harian: 0, tugas: 0, praktek: 0 };
            globalAttendance[nextId] = { hadir: 0, sakit: 0, izin: 0, alfa: 0 };
            syncAllPanels();
        }

        function editStudent(id) {
            const s = globalStudents.find(st => st.id === id); if (!s) return;
            s.nisn = prompt("Edit NISN:", s.nisn) || s.nisn;
            s.nama = (prompt("Edit Nama:", s.nama) || s.nama).toUpperCase();
            s.jk = prompt("Edit Jenis Kelamin:", s.jk) || s.jk;
            s.status = prompt("Edit Status:", s.status) || s.status;
            syncAllPanels();
        }

        function deleteStudent(id) {
            if(confirm("Hapus siswa ini?")) {
                globalStudents = globalStudents.filter(s => s.id !== id);
                syncAllPanels();
            }
        }

        function editStudentAttendance(id) {
            const att = globalAttendance[id]; const s = globalStudents.find(st => st.id === id);
            globalAttendance[id] = {
                hadir: parseInt(prompt("Hadir (Hari):", att.hadir)) || 0,
                sakit: parseInt(prompt("Sakit (Hari):", att.sakit)) || 0,
                izin: parseInt(prompt("Izin (Hari):", att.izin)) || 0,
                alfa: parseInt(prompt("Alfa (Hari):", att.alfa)) || 0
            };
            renderAbsenSiswa();
        }

        function editStudentGrade(id) {
            const g = globalGrades[id]; const s = globalStudents.find(st => st.id === id);
            globalGrades[id] = {
                harian: parseFloat(prompt("Nilai Harian:", g.harian)) || 0,
                tugas: parseFloat(prompt("Nilai Tugas:", g.tugas)) || 0,
                praktek: parseFloat(prompt("Nilai Praktek:", g.praktek)) || 0
            };
            renderNilaiSiswa();
        }

        function syncAllPanels() {
            renderDataSiswa(); renderAbsenSiswa(); renderNilaiSiswa(); renderJadwalPiket();
        }

        function renderDataSiswa() {
            const tbody = document.querySelector("#table-siswa tbody"); tbody.innerHTML = "";
            globalStudents.forEach((s, i) => {
                tbody.innerHTML += `<tr><td>${i+1}</td><td>${s.nisn}</td><td>${s.nama}</td><td>${s.jk}</td><td>${s.status}</td><td class="action-column"><div class="action-cells"><button class="btn btn-edit" onclick="editStudent(${s.id})">✏️</button><button class="btn btn-delete" onclick="deleteStudent(${s.id})">🗑️</button></div></td></tr>`;
            });
            setAdminVisibility(currentRole === "guru");
        }

        function renderAbsenSiswa() {
            const tbody = document.querySelector("#table-absen tbody"); tbody.innerHTML = "";
            globalStudents.forEach((s, i) => {
                const a = globalAttendance[s.id] || {hadir:0, sakit:0, izin:0, alfa:0};
                tbody.innerHTML += `<tr><td>${i+1}</td><td>${s.nama}</td><td>${a.hadir}</td><td>${a.sakit}</td><td>${a.izin}</td><td>${a.alfa}</td><td class="action-column"><button class="btn btn-edit" onclick="editStudentAttendance(${s.id})">✏️ Input</button></td></tr>`;
            });
            setAdminVisibility(currentRole === "guru");
        }

        function renderNilaiSiswa() {
            const tbody = document.querySelector("#table-nilai tbody"); tbody.innerHTML = "";
            globalStudents.forEach((s, i) => {
                const g = globalGrades[s.id] || {harian:0, tugas:0, praktek:0};
                const avg = ((g.harian + g.tugas + g.praktek) / 3).toFixed(1);
                tbody.innerHTML += `<tr><td>${i+1}</td><td>${s.nama}</td><td>${g.harian}</td><td>${g.tugas}</td><td>${g.praktek}</td><td><b>${avg}</b></td><td class="action-column"><button class="btn btn-edit" onclick="editStudentGrade(${s.id})">✏️ Input</button></td></tr>`;
            });
            setAdminVisibility(currentRole === "guru");
        }

        function renderJadwalPiket() {
            const tbody = document.querySelector("#table-piket tbody"); tbody.innerHTML = "";
            const hariList = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat", "Sabtu"];
            let kelompok = { "Senin":[], "Selasa":[], "Rabu":[], "Kamis":[], "Jumat":[], "Sabtu":[] };
            globalStudents.forEach((s, idx) => { kelompok[hariList[idx % hariList.length]].push(s.nama.split(' ')[0]); });
            hariList.forEach(h => { tbody.innerHTML += `<tr><td><b>${h}</b></td><td>${kelompok[h].join(", ") || "-"}</td></tr>`; });
        }

        function uploadGenericTable(input, tableId) {
            const file = input.files[0]; if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                const rows = e.target.result.split(/\r?\n/);
                const tbody = document.getElementById(tableId).querySelector('tbody'); tbody.innerHTML = "";
                rows.forEach((r, idx) => {
                    if (idx === 0 || r.trim() === "") return;
                    const cols = r.split(/[,;](?=(?:(?:[^"]*"){2})*[^"]*$)/);
                    let tr = document.createElement('tr');
                    cols.forEach(c => { let td = document.createElement('td'); td.innerText = c.replace(/"/g, "").trim(); tr.appendChild(td); });
                    tbody.appendChild(tr);
                });
                alert("Data tabel berhasil diperbarui.");
            };
            reader.readAsText(file); input.value = '';
        }

        function downloadData(tableId, filename) {
            const table = document.getElementById(tableId); let csv = [];
            let hasAction = table.querySelector(".action-column") && table.querySelector(".action-column").style.display !== "none";
            for (let i = 0; i < table.rows.length; i++) {
                let row = [], cols = table.rows[i].cells;
                let limit = hasAction ? cols.length - 1 : cols.length;
                for (let j = 0; j < limit; j++) { row.push('"' + cols[j].innerText.trim().replace(/"/g, '""') + '"'); }
                csv.push(row.join(","));
            }
            const blob = new Blob([ "\uFEFF" + csv.join("\n") ], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a"); link.href = URL.createObjectURL(blob);
            link.setAttribute("download", filename + ".csv"); document.body.appendChild(link); link.click(); document.body.removeChild(link);
        }
    </script>
</body>
</html>
