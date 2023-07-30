# Tutorial MERN untuk Pemula

MERN adalah singkatan dari MongoDB, Express, React, dan Node.js. Ini adalah tumpukan teknologi populer yang digunakan untuk mengembangkan aplikasi web modern. Dalam tutorial ini, kita akan memandu Anda langkah demi langkah untuk memulai dengan MERN dan membangun aplikasi web sederhana.

## Persiapan

Sebelum memulai, pastikan Anda telah menginstal Node.js dan NPM di komputer Anda. Anda juga harus memiliki editor teks atau IDE yang nyaman digunakan, seperti Visual Studio Code.

## Langkah 1: Inisialisasi Proyek

1. Buka terminal atau command prompt, dan buat direktori baru untuk proyek MERN Anda.

```
mkdir nama-proyek
cd nama-proyek
```

2. Inisialisasi proyek Node.js dengan perintah berikut:

```
npm init -y
```

## Langkah 2: Instalasi Paket-paket

Sekarang kita akan menginstal paket-paket yang diperlukan untuk proyek MERN kita.

1. Instal Express (Backend):

```
npm install express
```

2. Instal MongoDB (Database):

Unduh MongoDB dari situs resmi dan ikuti panduan instalasinya: https://www.mongodb.com/try/download/community

3. Instal Mongoose (ODM):

```
npm install mongoose
```

4. Instal React (Frontend):

```
npx create-react-app client
```

5. Instal Axios (Komunikasi Backend-Frontend):

```
cd client
npm install axios
```

## Langkah 3: Konfigurasi Server

1. Buat file `server.js` di direktori utama proyek Anda dan tambahkan kode berikut:

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');

const app = express();

// Middleware
app.use(cors());
app.use(express.json());

// MongoDB Connection
const dbURI = 'mongodb://localhost:27017/nama-database'; // Ganti dengan nama database yang diinginkan
mongoose.connect(dbURI, { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => app.listen(5000, () => console.log('Server berjalan di http://localhost:5000')))
    .catch((err) => console.log(err.message));
```

2. Ganti `nama-database` dengan nama database yang Anda inginkan. Pastikan MongoDB sudah berjalan di sistem Anda.

## Langkah 4: Konfigurasi Frontend

1. Di dalam direktori `client/src`, buka file `App.js` dan hapus semua kode yang ada, kemudian gantikan dengan kode berikut:

```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const App = () => {
    const [data, setData] = useState([]);

    useEffect(() => {
        fetchData();
    }, []);

    const fetchData = async () => {
        try {
            const response = await axios.get('http://localhost:5000/api/data'); // Ganti dengan URL API backend Anda
            setData(response.data);
        } catch (err) {
            console.log(err);
        }
    };

    return (
        <div>
            <h1>Data dari Server:</h1>
            {data.map((item) => (
                <p key={item._id}>{item.name}</p>
            ))}
        </div>
    );
};

export default App;
```

2. Di dalam direktori `client/src`, buka file `index.js` dan gantikan baris berikut:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>,
    document.getElementById('root')
);
```

## Langkah 5: Jalankan Proyek

1. Mulai server backend dengan menjalankan perintah berikut di terminal:

```
node server.js
```

2. Di direktori `client`, mulai server frontend dengan perintah:

```
npm start
```

3. Aplikasi MERN Anda sekarang akan berjalan di http://localhost:3000. Anda akan melihat data yang diambil dari server backend dan ditampilkan di aplikasi React frontend Anda.

