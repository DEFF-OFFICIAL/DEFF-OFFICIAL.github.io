<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simpan Data dengan Pilihan Hari</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            font-size: 18px;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .profile {
            display: flex;
            align-items: center;
        }
        .profile img {
            border-radius: 50%;
            width: 40px;
            height: 40px;
            margin-right: 10px;
        }
        .profile-name {
            font-size: 16px;
            color: white;
            font-weight: 600;
        }
        .logout-btn {
            background-color: #F44336;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }
        .logout-btn:hover {
            background-color: #D32F2F;
        }
        .container {
            max-width: 1000px;
            margin: 20px auto;
            padding: 10px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h1 {
            font-size: 16px;
            color: #333;
            margin-bottom: 10px;
        }
        form {
            margin-bottom: 20px;
        }
        label {
            font-weight: 600;
            margin-bottom: 5px;
            display: block;
            color: #555;
        }
        input[type="text"], input[type="number"], input[type="date"] {
            width: 100%;
            padding: 4px;
            margin: 5px 0;
            border-radius: 5px;
            border: 1px solid #ddd;
            font-size: 12px;
            background-color: #f9f9f9;
        }
        button {
            color: white;
            padding: 6px 8px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
            transition: background-color 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        button:hover {
            opacity: 0.9;
        }
        .btn-save {
            background-color: #1E88E5;
        }
        .btn-save:hover {
            background-color: #1565C0;
        }
        .btn-sort {
            background-color: #6D4C41;
        }
        .btn-sort:hover {
            background-color: #4E342E;
        }
        .btn-search {
            background-color: #FBC02D;
        }
        .btn-search:hover {
            background-color: #F9A825;
        }
        .btn-data-utama, .btn-data-berakhir, .btn-data-terhapus {
            width: 30%;
            padding: 10px;
            margin-top: 10px;
            font-size: 14px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .btn-data-utama {
            background-color: #2196F3;
        }
        .btn-data-utama:hover {
            background-color: #1976D2;
        }
        .btn-data-berakhir {
            background-color: #FF9800;
        }
        .btn-data-berakhir:hover {
            background-color: #FB8C00;
        }
        .btn-data-terhapus {
            background-color: #9E9E9E;
        }
        .btn-data-terhapus:hover {
            background-color: #757575;
        }
        .btn-edit {
            background-color: #4CAF50;
        }
        .btn-edit:hover {
            background-color: #43A047;
        }
        .btn-hapus {
            background-color: #F44336;
        }
        .btn-hapus:hover {
            background-color: #D32F2F;
        }
        .table-container {
            overflow-x: auto;
            margin-top: 10px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            font-size: 10px;
        }
        table, th, td {
            border: 1px solid #ddd;
            padding: 2px;
        }
        th {
            background-color: #4CAF50;
            color: white;
        }
        td:nth-child(1) {
            width: 4%;
            text-align: center;
        }
        td:nth-child(2) {
            width: 12%;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        td:nth-child(3) {
            width: 20%;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        td:nth-child(4), td:nth-child(5) {
            width: 9%;
            text-align: center;
            white-space: nowrap;
        }
        td:nth-child(6) {
            width: 8%;
            text-align: center;
            white-space: nowrap;
        }
        .sort-buttons, .search-section, .data-filters {
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
        }
        .sort-buttons button, .search-section input {
            margin-right: 5px;
        }
        .copy-icon {
            cursor: pointer;
            color: #4CAF50;
            font-size: 16px;
        }
        .notification {
            visibility: hidden;
            min-width: 250px;
            background-color: #4CAF50;
            color: white;
            text-align: center;
            border-radius: 5px;
            padding: 6px;
            position: fixed;
            z-index: 1;
            left: 50%;
            transform: translateX(-50%);
            bottom: 20px;
            font-size: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .notification.show {
            visibility: visible;
        }
        .button-group {
            display: flex;
            justify-content: space-between;
            gap: 8px;
            margin-top: 20px;
        }
        .copy-all-button, .delete-all-button {
            padding: 10px;
            border: none;
            cursor: pointer;
            font-size: 14px;
            text-align: center;
            border-radius: 8px;
            width: 30%;
            transition: background-color 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .copy-all-button {
            background-color: #673AB7;
        }
        .copy-all-button:hover {
            background-color: #5E35B1;
        }
        .delete-all-button {
            background-color: #E53935;
        }
        .delete-all-button:hover {
            background-color: #D32F2F;
        }
        @media only screen and (max-width: 600px) {
            body {
                font-size: 14px;
            }
            .container {
                width: 95%;
                padding: 10px;
            }
            table, th, td {
                font-size: 9px;
                padding: 3px;
            }
            .button-group button {
                font-size: 10px;
            }
        }
    </style>
</head>
<body>

<header>
    <div class="profile">
        <img id="profileImage" src="" alt="Profile Image">
        <span id="profileName" class="profile-name">Pengguna</span>
    </div>
    
    <h1>Dasboard Admin</h1>
    <button class="logout-btn" onclick="logout()">Logout</button>
</header>

<div class="container">
    <h1>Formulir Data Siluman</h1>
    <form id="dataForm">
        <label for="name">Nama:</label>
        <input type="text" id="name" required>

        <label for="hwid">Kode HWID:</label>
        <input type="text" id="hwid" required>

        <label for="days">Jumlah Hari:</label>
        <input type="number" id="days" min="1" max="365" required oninput="updateDates()">

        <label for="startDate">Tanggal Dibuat:</label>
        <input type="date" id="startDate" required readonly>

        <label for="endDate">Tanggal Berakhir:</label>
        <input type="date" id="endDate" required readonly>

        <button type="button" id="saveButton" class="btn-save" onclick="saveData()">Simpan Data</button>
        <input type="hidden" id="editIndex" value="">
    </form>

    <div class="data-filters button-group">
        <button type="button" class="btn-data-utama" onclick="displayData()">Data Utama</button>
        <button type="button" class="btn-data-berakhir" onclick="showExpiredData()">Data Tanggal Berakhir</button>
        <button type="button" class="btn-data-terhapus" onclick="showDeletedData()">Data Terhapus</button>
    </div>

    <div class="sort-buttons">
        <button class="btn-sort" onclick="sortByName()">Sortir A-Z</button>
        <button class="btn-sort" onclick="sortByEndDate()">Sortir Tanggal Berakhir</button>
        <div class="search-section">
            <input type="text" id="search" placeholder="Cari Nama..." oninput="filterByName()">
        </div>
    </div>

    <h2>Data yang Disimpan</h2>
    <div class="table-container">
        <table id="dataTable">
            <thead>
                <tr>
                    <th>No</th>
                    <th>Nama</th>
                    <th>Kode HWID</th>
                    <th>Tanggal Dibuat</th>
                    <th>Tanggal Berakhir</th>
                    <th>Aksi</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>

    <div class="button-group">
        <button class="copy-all-button" onclick="copyAllData()">Salin Semua Data Utama</button>
        <button class="delete-all-button" onclick="deleteAllExpired()">Hapus Semua Data Tanggal Berakhir</button>
        <button class="delete-all-button" onclick="deleteAllDeleted()">Hapus Semua Data Terhapus</button>
    </div>
</div>

<div id="notification" class="notification">Data berhasil disalin!</div>

<script>
    // Cek sesi login
    const currentUser = JSON.parse(localStorage.getItem('currentUser'));
    if (!currentUser) {
        alert('Anda harus login terlebih dahulu!');
        window.location.href = 'login.html'; // Arahkan ke halaman login jika belum login
    } else {
        // Tampilkan nama dan gambar profil
        document.getElementById('profileName').textContent = currentUser.name;
        document.getElementById('profileImage').src = currentUser.profileImage || 'https://via.placeholder.com/50';
    }

    // Fungsi logout
    function logout() {
        localStorage.removeItem('currentUser'); // Hapus data pengguna dari localStorage
        window.location.href = 'login.html'; // Arahkan kembali ke halaman login
    }

    let isEditing = false;
    let deletedDataList = JSON.parse(localStorage.getItem('deletedDataList')) || [];

    function updateDates() {
        const days = parseInt(document.getElementById('days').value);
        if (isNaN(days) || days < 1) return;

        const now = new Date();
        const startDate = new Date(now);
        const endDate = new Date(now);
        endDate.setDate(now.getDate() + days - 1);

        const startDateStr = startDate.toISOString().split('T')[0];
        const endDateStr = endDate.toISOString().split('T')[0];

        document.getElementById('startDate').value = startDateStr;
        document.getElementById('endDate').value = endDateStr;
    }

    function saveData() {
        const name = document.getElementById('name').value;
        const hwid = document.getElementById('hwid').value;
        const startDate = document.getElementById('startDate').value;
        const endDate = document.getElementById('endDate').value;
        const editIndex = document.getElementById('editIndex').value;

        if (!name || !hwid || !startDate || !endDate) {
            alert('Semua kolom harus diisi.');
            return;
        }

        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];

        const isDuplicateName = dataList.some(data => data.name.toLowerCase() === name.toLowerCase());

        if (isDuplicateName) {
            showNotification('Nama ini sudah ada!');
            return;
        }

        if (isEditing) {
            dataList[editIndex] = { name, hwid, startDate, endDate };
            isEditing = false;
            document.getElementById('saveButton').textContent = 'Simpan Data';
        } else {
            dataList.push({ name, hwid, startDate, endDate });
        }

        localStorage.setItem('dataList', JSON.stringify(dataList));
        displayData();
        resetForm();
    }

    function resetForm() {
        document.getElementById('name').value = '';
        document.getElementById('hwid').value = '';
        document.getElementById('days').value = '';
        document.getElementById('startDate').value = '';
        document.getElementById('endDate').value = '';
        document.getElementById('editIndex').value = '';
    }

    function deleteData(index) {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        let deletedItem = dataList.splice(index, 1)[0];
        deletedDataList.push(deletedItem);
        localStorage.setItem('dataList', JSON.stringify(dataList));
        localStorage.setItem('deletedDataList', JSON.stringify(deletedDataList));
        displayData();
    }

    function editData(index) {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        const data = dataList[index];

        document.getElementById('name').value = data.name;
        document.getElementById('hwid').value = data.hwid;
        document.getElementById('startDate').value = data.startDate;
        document.getElementById('endDate').value = data.endDate;
        document.getElementById('editIndex').value = index;

        document.getElementById('saveButton').textContent = 'Update Data';
        isEditing = true;
    }

    function restoreData(index) {
        let deletedData = deletedDataList.splice(index, 1)[0];
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        dataList.push(deletedData);
        localStorage.setItem('dataList', JSON.stringify(dataList));
        localStorage.setItem('deletedDataList', JSON.stringify(deletedDataList));
        showDeletedData();
    }

    function deletePermanently(index) {
        deletedDataList.splice(index, 1);
        localStorage.setItem('deletedDataList', JSON.stringify(deletedDataList));
        showDeletedData();
    }

    function deleteAllExpired() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        const now = new Date();
        dataList = dataList.filter(data => new Date(data.endDate) >= now);
        localStorage.setItem('dataList', JSON.stringify(dataList));
        showExpiredData();
    }

    function deleteAllDeleted() {
        deletedDataList = [];
        localStorage.setItem('deletedDataList', JSON.stringify(deletedDataList));
        showDeletedData();
    }

    function copyToClipboard(text, fieldName) {
        const tempInput = document.createElement('input');
        tempInput.style.position = 'absolute';
        tempInput.style.left = '-9999px';
        tempInput.value = text;
        document.body.appendChild(tempInput);
        tempInput.select();
        document.execCommand('copy');
        document.body.removeChild(tempInput);

        showNotification(`${fieldName} sudah disalin ke papan klip`);
    }

    function showNotification(message) {
        const notification = document.getElementById('notification');
        notification.textContent = message;
        notification.className = "notification show";

        setTimeout(() => {
            notification.className = "notification";
        }, 2000);
    }

    function displayData() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        const dataTableBody = document.querySelector('#dataTable tbody');
        dataTableBody.innerHTML = '';

        dataList.forEach((data, index) => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${index + 1}</td>
                <td>
                    ${data.name}
                    <span class="copy-icon" onclick="copyToClipboard('${data.name}', 'Nama')">📋</span>
                </td>
                <td>
                    ${data.hwid}
                    <span class="copy-icon" onclick="copyToClipboard('${data.hwid}', 'Kode HWID')">📋</span>
                </td>
                <td>${data.startDate}</td>
                <td>${data.endDate}</td>
                <td class="action-buttons">
                    <button class="btn-edit" onclick="editData(${index})">Edit</button>
                    <button class="btn-hapus" onclick="deleteData(${index})">Hapus</button>
                </td>
            `;
            dataTableBody.appendChild(row);
        });
    }

    function showExpiredData() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        const dataTableBody = document.querySelector('#dataTable tbody');
        dataTableBody.innerHTML = '';
        const now = new Date();

        dataList.forEach((data, index) => {
            const endDate = new Date(data.endDate);
            if (endDate < now) {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${data.name}</td>
                    <td>${data.hwid}</td>
                    <td>${data.startDate}</td>
                    <td>${data.endDate}</td>
                    <td class="action-buttons">
                        <button class="btn-edit" onclick="editData(${index})">Edit</button>
                        <button class="btn-hapus" onclick="deleteData(${index})">Hapus</button>
                        <button class="btn-hapus" onclick="deletePermanently(${index})">Hapus Permanen</button>
                    </td>
                `;
                dataTableBody.appendChild(row);
            }
        });
    }

    function showDeletedData() {
        const dataTableBody = document.querySelector('#dataTable tbody');
        dataTableBody.innerHTML = '';

        deletedDataList.forEach((data, index) => {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${index + 1}</td>
                <td>${data.name}</td>
                <td>${data.hwid}</td>
                <td>${data.startDate}</td>
                <td>${data.endDate}</td>
                <td class="action-buttons">
                    <button class="btn-edit" onclick="restoreData(${index})">Pulihkan</button>
                    <button class="btn-hapus" onclick="deletePermanently(${index})">Hapus Permanen</button>
                </td>
            `;
            dataTableBody.appendChild(row);
        });
    }

    function copyAllData() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        let textToCopy = "No\tNama\tKode HWID\tTanggal Dibuat\tTanggal Berakhir\n";

        dataList.forEach((data, index) => {
            textToCopy += `${index + 1}\t${data.name}\t${data.hwid}\t${data.startDate}\t${data.endDate}\n`;
        });

        const tempInput = document.createElement('textarea');
        tempInput.value = textToCopy;
        document.body.appendChild(tempInput);
        tempInput.select();
        document.execCommand('copy');
        document.body.removeChild(tempInput);

        showNotification('Data berhasil disalin!');
    }

    function sortByName() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        dataList.sort((a, b) => a.name.localeCompare(b.name));
        localStorage.setItem('dataList', JSON.stringify(dataList));
        displayData();
    }

    function sortByEndDate() {
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        dataList.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
        localStorage.setItem('dataList', JSON.stringify(dataList));
        displayData();
    }

    function filterByName() {
        const searchValue = document.getElementById('search').value.toLowerCase();
        let dataList = JSON.parse(localStorage.getItem('dataList')) || [];
        const dataTableBody = document.querySelector('#dataTable tbody');
        dataTableBody.innerHTML = '';

        dataList.forEach((data, index) => {
            if (data.name.toLowerCase().includes(searchValue)) {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>
                        ${data.name}
                        <span class="copy-icon" onclick="copyToClipboard('${data.name}', 'Nama')">📋</span>
                    </td>
                    <td>
                        ${data.hwid}
                        <span class="copy-icon" onclick="copyToClipboard('${data.hwid}', 'Kode HWID')">📋</span>
                    </td>
                    <td>${data.startDate}</td>
                    <td>${data.endDate}</td>
                    <td class="action-buttons">
                        <button class="btn-edit" onclick="editData(${index})">Edit</button>
                        <button class="btn-hapus" onclick="deleteData(${index})">Hapus</button>
                    </td>
                `;
                dataTableBody.appendChild(row);
            }
        });
    }

    displayData();
</script>
</body>
</html>
