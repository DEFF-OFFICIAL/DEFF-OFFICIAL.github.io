<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Admin</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            max-width: 400px;
            width: 100%;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            box-sizing: border-box;
        }
        h1 {
            text-align: center;
            color: #333;
            font-size: 24px;
            margin-bottom: 20px;
        }
        label {
            font-size: 14px;
            font-weight: bold;
            color: #333;
            margin-bottom: 5px;
            display: block;
        }
        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            box-sizing: border-box;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #43A047;
        }
        .message {
            color: red;
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Login Admin</h1>
    <form id="loginForm">
        <label for="email">Email Admin:</label>
        <input type="email" id="email" placeholder="Masukkan email" required>

        <label for="password">Kata Sandi:</label>
        <input type="password" id="password" placeholder="Masukkan kata sandi" required>

        <button type="submit">Login</button>

        <div id="message" class="message"></div>
    </form>
</div>

<script>
    // Data akun owner permanen (DEFF STORE) untuk login sebagai Owner
    const permanentOwner = {
        name: "DEFF STORE",
        email: "husnulrijal09@gmail.com",
        password: "Kartuku09",
        profileImage: "https://via.placeholder.com/50" // URL gambar profil untuk Owner
    };

    // Simpan akun permanen ke localStorage hanya jika adminData belum ada
    if (!localStorage.getItem('adminData')) {
        localStorage.setItem('adminData', JSON.stringify([permanentOwner]));
    } else {
        // Pastikan akun permanen tersimpan jika belum ada di data admin
        let adminData = JSON.parse(localStorage.getItem('adminData'));
        const isPermanentOwnerExist = adminData.some(admin => admin.email === permanentOwner.email);

        if (!isPermanentOwnerExist) {
            adminData.push(permanentOwner);
            localStorage.setItem('adminData', JSON.stringify(adminData));
        }
    }

    // Fungsi untuk login
    document.getElementById('loginForm').addEventListener('submit', function(e) {
        e.preventDefault();

        const email = document.getElementById('email').value.trim();
        const password = document.getElementById('password').value.trim();

        // Ambil semua akun admin dari localStorage
        const adminData = JSON.parse(localStorage.getItem('adminData')) || [];

        // Cek apakah ada admin dengan email dan password yang cocok
        const admin = adminData.find(admin => admin.email === email && admin.password === password);

        if (admin) {
            // Simpan data admin yang login ke localStorage sebagai pengguna yang aktif
            localStorage.setItem('currentUser', JSON.stringify(admin));

            // Arahkan ke halaman owner jika login sebagai DEFF STORE (Owner)
            if (admin.email === permanentOwner.email) {
                window.location.href = 'owner.html'; // Arahkan ke halaman Owner
            } else {
                // Jika bukan DEFF STORE, arahkan ke halaman admin-dashboard
                window.location.href = 'admin-dashboard.html';
            }
        } else {
            // Tampilkan pesan error jika email atau password salah
            document.getElementById('message').textContent = "Email atau kata sandi salah!";
        }
    });
</script>

</body>
</html>
