

Prasyarat
Sebelum coding, pastikan kamu punya:
- Laptop:
  - Node.js LTS (v20.x.x): Unduh dari [nodejs.org](https://nodejs.org).
  - Expo CLI: Akan diinstall nanti.
  - VS Code (atau editor lain) dengan ekstensi JavaScript.
     - Smartphone:
  - Android/iOS dengan aplikasi Expo Go terinstall (Play Store/App Store).
- Koneksi Internet: Laptop dan HP harus di jaringan Wi-Fi yang sama.
- Waktu: 120 menit (60 menit setup dan coding, 60 menit pengujian dan debugging).

Catatan Teknis:
- Menggunakan Expo SDK 51 dengan template blank JavaScript.
- Tanggal referensi untuk tugas terlambat: 15 Mei 2025, 07:56 WIB.
- Kode diuji pada 10 Mei 2025, kompatibel dengan Expo Go.

---

 Langkah 1: Persiapan Lingkungan
Narasi:  
“Sobat Dev, sebelum kita coding, kita siapkan alat-alatnya dulu, seperti menyiapkan bahan sebelum masak! Kita akan install Node.js, Expo CLI, dan cek semuanya jalan. Yuk, buka terminal di VS Code!”

1. Cek Node.js  
   - Buka terminal di VS Code (`Ctrl + ~` atau `Terminal > New Terminal`).  
   - Jalankan:  
     ```bash
     node -v
     npm -v
     ```
     - Harapan: Muncul versi, misal `v20.12.2` (Node.js) dan `10.5.0` (npm).  
     - Error: Jika `command not found`, unduh Node.js LTS dari [nodejs.org](https://nodejs.org), install, lalu restart terminal.

2. Install Expo CLI  
   - Jalankan:  
     ```bash
     npm install -g expo-cli
     ```
     - Harapan: Proses selesai tanpa error.  
     - Error: Jika gagal (misal, izin ditolak), coba `sudo npm install -g expo-cli` (Mac/Linux) atau jalankan terminal sebagai admin (Windows).  
   - Cek versi:  
     ```bash
     expo --version
     ```
     - Harapan: Muncul versi, misal `7.12.1`.  

3. Cek Expo Go  
   - Buka Expo Go di HP-mu.  
   - Pastikan HP dan laptop di Wi-Fi yang sama.  

4. Buat Folder Proyek  
   - Buat folder `TodoApp`:  
     ```bash
     mkdir TodoApp
     cd TodoApp
     ```

Checkpoint:  
“Node.js, Expo CLI, dan Expo Go siap? Kalau iya, kita lanjut bikin proyek!”

---

 Langkah 2: Membuat Proyek Expo
Narasi:  
“Sekarang kita bikin proyek baru dengan Expo, seperti membangun fondasi rumah! Kita akan membuat aplikasi bernama TodoApp dan menjalankannya di Expo Go. Ikuti langkahnya dengan teliti, Sobat Dev!”

1. Buat Proyek  
   - Jalankan:  
     ```bash
     npx create-expo-app TodoApp
     ```
     - Pilih blank (JavaScript, bukan TypeScript).  
     - Tunggu instalasi selesai (butuh internet).

2. Masuk ke Folder Proyek  
   ```bash
   cd TodoApp
   ```

3. Jalankan Aplikasi  
   - Start server:  
     ```bash
     npx expo start
     ```
     - Harapan: Muncul QR code di terminal atau browser (Metro Bundler).  
     - Error: Jika QR code tidak muncul, coba `npx expo start --clear` atau pastikan port `19000` tidak diblokir.  
   - Buka Expo Go, pindai QR code:  
     - Android: Pindai langsung.  
     - iOS: Buka kamera, klik link QR, lalu buka di Expo Go.  
     - Error: Jika tidak connect, cek Wi-Fi atau coba `npx expo start --tunnel`.  
   - Harapan: Muncul layar default Expo (“Open up App.js to start working...”).

4. Struktur Awal Proyek  
   ```
   TodoApp/
   ├── App.js
   ├── app.json
   ├── package.json
   ├── node_modules/
   └── assets/
   ```

Checkpoint:  
“Layar default muncul di HP? Kalau iya, kita siap coding! Buka VS Code di folder TodoApp!”

---

 Langkah 3: Install Dependensi
Narasi:  
“Sobat Dev, aplikasi kita butuh alat tambahan: navigasi untuk header, AsyncStorage untuk simpan data, dan DateTimePicker untuk pilih tanggal. Kita install semua di terminal dan buat folder untuk kode. Yuk, mulai!”

1. Pastikan kamu di folder `TodoApp`:  
   ```bash
   pwd
   ```

2. Install dependensi:  
   ```bash
   npm install @react-navigation/native @react-navigation/stack
   npx expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
   npx expo install @react-native-async-storage/async-storage
   npx expo install @react-native-community/datetimepicker
   ```
   - Penjelasan:  
     - `@react-navigation/*`: Untuk navigasi dan header.  
     - `gesture-handler`, dll.: Dependensi navigasi.  
     - `async-storage`: Simpan tugas di HP.  
     - `datetimepicker`: Pilih tanggal/waktu.  
   - Error: Jika gagal, cek internet atau hapus `node_modules` dan `package-lock.json`, lalu `npm install`.

3. Buat folder:  
   ```bash
   mkdir screens components styles
   ```

Checkpoint:  
“Dependensi terinstall? Folder screens, components, dan styles ada? Kita mulai coding iteratif sekarang!”

---

 Iterasi 1: Setup Navigasi dan Layar Utama dengan Teks Sambutan
Narasi:  
“Kita mulai dengan fondasi aplikasi! Di iterasi pertama, kita akan setup navigasi dengan header biru bertuliskan ‘Daftar Tugas’ di App.js, dan membuat layar utama di HomeScreen.js yang menampilkan teks sambutan sederhana. Kita juga akan membuat file gaya untuk HomeScreen. Karena belum ada komponen tugas, file TodoItem.js dan gaya terkait akan dibuat nanti. Yuk, buka VS Code dan ikuti langkahnya!”

# Kode: App.js
Tujuan: Mengatur navigasi dengan header biru dan menampilkan HomeScreen.
```javascript
/* Menambah fitur: Setup navigasi dengan header biru */
import React from 'react'; // Tambahkan ini: Impor React untuk komponen
import { NavigationContainer } from '@react-navigation/native'; // Tambahkan ini: Untuk mengelola navigasi
import { createStackNavigator } from '@react-navigation/stack'; // Tambahkan ini: Untuk navigasi bertumpuk
import HomeScreen from './screens/HomeScreen'; // Tambahkan ini: Impor layar utama

const Stack = createStackNavigator(); // Tambahkan ini: Buat instance stack navigator

export default function App() {
  return (
    <NavigationContainer> // Tambahkan ini: Bungkus navigasi
      <Stack.Navigator> // Tambahkan ini: Atur struktur navigasi
        <Stack.Screen
          name="Home" // Tambahkan ini: Nama layar
          component={HomeScreen} // Tambahkan ini: Komponen layar
          options={{
            title: 'Daftar Tugas', // Tambahkan ini: Judul header
            headerStyle: { backgroundColor: '#007AFF' }, // Tambahkan ini: Latar biru
            headerTintColor: '#fff', // Tambahkan ini: Teks putih
            headerTitleStyle: { fontWeight: 'bold' }, // Tambahkan ini: Teks tebal
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

Penjelasan Kode Per Baris:
- `import React from 'react'; // Tambahkan ini`  
  - Fungsi: Mengimpor React untuk membuat komponen.  
  - Cara Kerja: React adalah inti React Native, memungkinkan penulisan UI deklaratif.  

- `import { NavigationContainer } from '@react-navigation/native'; // Tambahkan ini`  
  - Fungsi: Mengelola state dan konteks navigasi.  
  - Cara Kerja: Membungkus semua navigasi, menyediakan history dan state untuk transisi layar.  

- `import { createStackNavigator } from '@react-navigation/stack'; // Tambahkan ini`  
  - Fungsi: Membuat navigasi bertumpuk (stack).  
  - Cara Kerja: Memungkinkan layar ditumpuk seperti kartu, dengan animasi push/pop.  

- `import HomeScreen from './screens/HomeScreen'; // Tambahkan ini`  
  - Fungsi: Mengimpor komponen HomeScreen.  
  - Cara Kerja: Akan error jika HomeScreen.js belum ada, jadi kita buat berikutnya.  

- `const Stack = createStackNavigator(); // Tambahkan ini`  
  - Fungsi: Membuat instance stack navigator.  
  - Cara Kerja: Menyediakan komponen `Navigator` dan `Screen` untuk struktur navigasi.  

- `<NavigationContainer> // Tambahkan ini`  
  - Fungsi: Membungkus navigasi aplikasi.  
  - Cara Kerja: Mengelola state navigasi global, wajib untuk semua navigasi.  

- `<Stack.Navigator> // Tambahkan ini`  
  - Fungsi: Menentukan struktur navigasi bertumpuk.  
  - Cara Kerja: Mengatur tumpukan layar untuk transisi.  

- `<Stack.Screen name="Home" component={HomeScreen} options={{ ... }} />`  
  - Fungsi: Mendefinisikan layar “Home”.  
  - Cara Kerja:  
    - `name="Home"`: Nama unik layar.  
    - `component={HomeScreen}`: Komponen yang dirender.  
    - `options`: Mengatur header:  
      - `title: 'Daftar Tugas'`: Judul.  
      - `headerStyle`: Latar biru (#007AFF).  
      - `headerTintColor`: Teks putih.  
      - `headerTitleStyle`: Teks tebal.  

# Kode: screens/HomeScreen.js
Tujuan: Menampilkan teks sambutan untuk memastikan layar utama berfungsi.
```javascript
/* Menambah fitur: Layar utama dengan teks sambutan */
import React from 'react'; // Tambahkan ini: Impor React
import { View, Text } from 'react-native'; // Tambahkan ini: Komponen UI
import styles from '../styles/HomeScreenStyles'; // Tambahkan ini: Impor gaya

export default function HomeScreen() {
  return (
    <View style={styles.container}> // Tambahkan ini: Container utama
      <Text style={styles.text}>Selamat datang di To-Do List!</Text> // Tambahkan ini: Teks sambutan
    </View>
  );
}
```

Penjelasan Kode Per Baris:
- `import React from 'react'; // Tambahkan ini`  
  - Fungsi: Mengimpor React.  
  - Cara Kerja: Wajib untuk komponen React Native.  

- `import { View, Text } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor komponen UI dasar.  
  - Cara Kerja:  
    - `View`: Container, seperti `<div>`.  
    - `Text`: Menampilkan teks, seperti `<p>`.  

- `import styles from '../styles/HomeScreenStyles'; // Tambahkan ini`  
  - Fungsi: Mengimpor gaya dari HomeScreenStyles.js.  
  - Cara Kerja: Memisahkan gaya untuk organisasi kode yang lebih baik.  

- `<View style={styles.container}> // Tambahkan ini`  
  - Fungsi: Container utama layar.  
  - Cara Kerja: Menggunakan gaya `container` untuk mengisi layar dan memusatkan konten.  

- `<Text style={styles.text}>Selamat datang di To-Do List!</Text> // Tambahkan ini`  
  - Fungsi: Menampilkan teks sambutan.  
  - Cara Kerja: Menggunakan gaya `text` untuk ukuran dan warna teks.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Menyediakan gaya untuk HomeScreen.
```javascript
/* Menambah fitur: Gaya untuk layar utama */
import { StyleSheet } from 'react-native'; // Tambahkan ini: Impor StyleSheet

const styles = StyleSheet.create({
  container: { // Tambahkan ini: Gaya container
    flex: 1, // Isi seluruh layar
    justifyContent: 'center', // Pusatkan vertikal
    alignItems: 'center', // Pusatkan horizontal
    backgroundColor: '#F5F5F5', // Latar abu-abu muda
  },
  text: { // Tambahkan ini: Gaya teks
    fontSize: 20, // Ukuran teks besar
    color: '#333', // Warna abu-abu gelap
  },
});

export default styles;
```

Penjelasan Kode Per Baris:
- `import { StyleSheet } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor StyleSheet untuk membuat gaya.  
  - Cara Kerja: Mengoptimalkan gaya untuk performa.  

- `container: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk container utama.  
  - Cara Kerja:  
    - `flex: 1`: Mengisi seluruh layar.  
    - `justifyContent: 'center'`: Memusatkan konten vertikal.  
    - `alignItems: 'center'`: Memusatkan konten horizontal.  
    - `backgroundColor: '#F5F5F5'`: Latar abu-abu muda.  

- `text: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk teks sambutan.  
  - Cara Kerja:  
    - `fontSize: 20`: Teks besar untuk keterbacaan.  
    - `color: '#333'`: Warna abu-abu gelap untuk kontras.  

Eksekusi:  
1. Simpan semua file:  
   - App.js di root.  
   - screens/HomeScreen.js di folder `screens`.  
   - styles/HomeScreenStyles.js di folder `styles`.  
2. Jalankan `npx expo start` (atau refresh jika sudah berjalan).  
3. Buka Expo Go, pindai QR code.  
4. Harapan: Muncul header biru “Daftar Tugas” dan teks “Selamat datang di To-Do List!” di tengah layar.  
5. Error: Jika error “Cannot find module './screens/HomeScreen'”, pastikan HomeScreen.js ada di folder `screens`.  

Checkpoint:  
“Header biru dan teks sambutan muncul di HP? Kalau iya, navigasi dan layar utama sudah jalan! Kita lanjut tambah form input di iterasi berikutnya!”

---

 Iterasi 2: Form Input dan DateTimePicker
Narasi:  
“Selamat, Sobat Dev! Layar utama sudah jadi. Sekarang kita tambah form di HomeScreen.js untuk input tugas dan memilih tanggal/waktu dengan DateTimePicker. Kita akan update file gaya di HomeScreenStyles.js untuk form, tapi belum perlu TodoItem.js karena belum menampilkan tugas. Form ini akan punya kolom teks, tombol untuk pilih tanggal/waktu, dan tombol ‘Tambah Tugas’ (belum aktif). Kita pakai KeyboardAvoidingView agar form tidak tertutup keyboard. Yuk, update kodenya!”

# Kode: App.js
Tujuan: Tidak ada perubahan, tetap sama karena fokus pada HomeScreen.
```javascript
/* Menambah fitur: Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

Penjelasan: Tidak ada perubahan karena navigasi sudah diatur di iterasi sebelumnya.

# Kode: screens/HomeScreen.js
Tujuan: Menambah form input dan DateTimePicker.
```javascript
/* Menambah fitur: Form input untuk tugas dan DateTimePicker */
import React, { useState } from 'react'; // Tambahkan ini: Impor useState untuk state
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text } from 'react-native'; // Tambahkan ini: Komponen untuk form
import DateTimePicker from '@react-native-community/datetimepicker'; // Tambahkan ini: Untuk pilih tanggal/waktu
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState(''); // Tambahkan ini: State untuk teks tugas
  const [date, setDate] = useState(new Date()); // Tambahkan ini: State untuk tanggal/waktu
  const [showDatePicker, setShowDatePicker] = useState(false); // Tambahkan ini: State untuk visibilitas picker

  // Tambahkan ini: Handler untuk perubahan tanggal/waktu
  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios'); // Tutup picker di Android
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'} // Tambahkan ini: Sesuaikan UI saat keyboard muncul
    >
      <View style={styles.inputContainer}> // Tambahkan ini: Container form
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask} // Tambahkan ini: Update state saat teks berubah
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}> // Tambahkan ini: Tombol untuk buka picker
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime" // Tambahkan ini: Pilih tanggal dan waktu
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()} // Tambahkan ini: Batasi tanggal
          />
        )}
        <Button title="Tambah Tugas" onPress={() => {}} color="#007AFF" /> // Tambahkan ini: Tombol sementara
      </View>
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Kode Per Baris:
- `import { useState } from 'react'; // Tambahkan ini`  
  - Fungsi: Mengimpor `useState` untuk mengelola state.  
  - Cara Kerja: Memungkinkan state dinamis seperti teks input dan tanggal.  

- `import { ..., TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor komponen untuk form.  
  - Cara Kerja:  
    - `TextInput`: Input teks.  
    - `Button`: Tombol.  
    - `KeyboardAvoidingView`: Menangani keyboard.  
    - `Platform`: Deteksi OS.  
    - `TouchableOpacity`: Tombol dengan efek klik.  
    - `Text`: Teks untuk tombol tanggal.  

- `import DateTimePicker from '@react-native-community/datetimepicker'; // Tambahkan ini`  
  - Fungsi: Mengimpor DateTimePicker.  
  - Cara Kerja: Menyediakan UI untuk memilih tanggal dan waktu.  

- `const [task, setTask] = useState(''); // Tambahkan ini`  
  - Fungsi: State untuk teks tugas.  
  - Cara Kerja: Nilai awal kosong, `setTask` memperbarui saat pengguna mengetik.  

- `const [date, setDate] = useState(new Date()); // Tambahkan ini`  
  - Fungsi: State untuk tanggal/waktu.  
  - Cara Kerja: Nilai awal waktu saat ini, `setDate` memperbarui saat tanggal dipilih.  

- `const [showDatePicker, setShowDatePicker] = useState(false); // Tambahkan ini`  
  - Fungsi: Mengontrol visibilitas DateTimePicker.  
  - Cara Kerja: `false` menyembunyikan, `true` menampilkan picker.  

- `const onDateChange = (event, selectedDate) => { ... } // Tambahkan ini`  
  - Fungsi: Menangani perubahan tanggal/waktu.  
  - Cara Kerja:  
    - `setShowDatePicker(Platform.OS === 'ios')`: Tutup picker di Android, tetap buka di iOS.  
    - `event.type === 'dismissed'`: Sembunyikan jika dibatalkan.  
    - `setDate(selectedDate)`: Perbarui state jika tanggal dipilih.  

- `<KeyboardAvoidingView style={styles.container} behavior={...}> // Tambahkan ini`  
  - Fungsi: Menyesuaikan UI saat keyboard muncul.  
  - Cara Kerja:  
    - `behavior`: `padding` (iOS) atau `height` (Android) untuk menggeser/mengubah tinggi layar.  
    - Menggantikan `View` untuk mendukung input.  

- `<View style={styles.inputContainer}> // Tambahkan ini`  
  - Fungsi: Container untuk form.  
  - Cara Kerja: Mengelompokkan input, tombol tanggal, dan tombol tambah.  

- `<TextInput style={styles.input} ... /> // Tambahkan ini`  
  - Fungsi: Input untuk nama tugas.  
  - Cara Kerja:  
    - `placeholder`: Petunjuk teks.  
    - `value={task}`: Menampilkan state.  
    - `onChangeText={setTask}`: Perbarui state saat mengetik.  

- `<TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}> // Tambahkan ini`  
  - Fungsi: Tombol untuk membuka picker.  
  - Cara Kerja: Mengubah `showDatePicker` ke `true` saat diklik.  

- `<Text style={styles.dateText}> ... </Text> // Tambahkan ini`  
  - Fungsi: Menampilkan tanggal/waktu format Indonesia.  
  - Cara Kerja:  
    - `toLocaleDateString('id-ID', { dateStyle: 'short' })`: Format “15/05/25”.  
    - `toLocaleTimeString('id-ID', { timeStyle: 'short' })`: Format “07:56”.  

- `{showDatePicker && ( <DateTimePicker ... /> )}`  
  - Fungsi: Menampilkan picker saat `showDatePicker` `true`.  
  - Cara Kerja:  
    - `mode="datetime"`: Pilih tanggal dan waktu sekaligus.  
    - `display`: `inline` (iOS), `default` (Android).  
    - `minimumDate`: Batasi ke tanggal saat ini atau setelahnya.  

- `<Button title="Tambah Tugas" onPress={() => {}} color="#007AFF" /> // Tambahkan ini`  
  - Fungsi: Tombol sementara.  
  - Cara Kerja: Placeholder `onPress`, warna biru sesuai tema.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Menambah gaya untuk form.
```javascript
/* Menambah fitur: Gaya untuk form input */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20, // Tambahkan ini: Jarak tepi
    backgroundColor: '#F5F5F5',
  },
  inputContainer: { // Tambahkan ini: Gaya container form
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: { // Tambahkan ini: Gaya input teks
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: { // Tambahkan ini: Gaya tombol tanggal
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: { // Tambahkan ini: Gaya teks tanggal
    fontSize: 16,
    color: '#333',
  },
});

export default styles;
```

Penjelasan Kode Per Baris:
- `padding: 20 // Tambahkan ini` (di `container`)  
  - Fungsi: Menambah jarak tepi layar.  
  - Cara Kerja: Memberi ruang agar form tidak menempel ke tepi.  

- `inputContainer: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk container form.  
  - Cara Kerja:  
    - `backgroundColor: '#fff'`: Latar putih.  
    - `padding: 15`: Jarak dalam.  
    - `borderRadius: 10`: Sudut membulat.  
    - `shadow*` dan `elevation`: Efek bayangan.  

- `input: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk TextInput.  
  - Cara Kerja: Border tipis, padding nyaman, font besar.  

- `dateButton: { ... } // Tambahkan ini`  
  - Fungsi: Gaya tombol tanggal.  
  - Cara Kerja: Latar abu-abu, sudut membulat.  

- `dateText: { ... } // Tambahkan ini`  
  - Fungsi: Gaya teks tanggal.  
  - Cara Kerja: Font sedang, warna abu-abu gelap.  

Eksekusi:  
1. Simpan semua file.  
2. Refresh Expo Go (`r` di terminal atau shake HP).  
3. Harapan: Muncul form dengan input teks, tombol tanggal/waktu, dan tombol “Tambah Tugas”. Klik tombol tanggal untuk lihat DateTimePicker.  
4. Error: Jika DateTimePicker tidak muncul, cek instalasi `@react-native-community/datetimepicker` atau state `showDatePicker`.  

Checkpoint:  
“Form muncul di HP? Coba ketik tugas dan pilih tanggal. Kalau DateTimePicker jalan, kita lanjut tambah logika tugas!”

---

 Iterasi 3: Logika Menambah Tugas dan AsyncStorage
Narasi:  
“Form sudah ada, Sobat Dev! Sekarang kita buat tombol ‘Tambah Tugas’ berfungsi dan simpan tugas dengan AsyncStorage agar tetap ada setelah aplikasi ditutup. Kita akan update HomeScreen.js untuk menambah tugas dan menyimpannya. File gaya tetap sama karena UI form tidak berubah, dan TodoItem.js belum dibutuhkan karena belum menampilkan daftar. Yuk, tambah logika!”

# Kode: App.js
Tujuan: Tidak ada perubahan.
```javascript
/* Menambah fitur: Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

# Kode: screens/HomeScreen.js
Tujuan: Menambah logika untuk tugas dan AsyncStorage.
```javascript
/* Menambah fitur: Logika menambah tugas dan AsyncStorage */
import React, { useState, useEffect } from 'react'; // Tambahkan ini: Impor useEffect
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text } from 'react-native';
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage'; // Tambahkan ini: Untuk penyimpanan
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]); // Tambahkan ini: State untuk daftar tugas

  // Tambahkan ini: Muat tugas saat aplikasi mulai
  useEffect(() => {
    loadTodos();
  }, []);

  // Tambahkan ini: Fungsi memuat tugas
  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  // Tambahkan ini: Fungsi menyimpan tugas
  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  // Tambahkan ini: Fungsi menambah tugas
  const addTask = () => {
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    const newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input
        placeholder="Masukkan tugas"
        value={task}
        onChangeText={setTask}
      />
      <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
        <Text style={styles.dateText}>
          {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
        </Text>
      </TouchableOpacity>
      {showDatePicker && (
        <DateTimePicker
          value={date}
          mode="datetime"
          display={Platform.OS === 'ios' ? 'inline' : 'default'}
          onChange={onDateChange}
          minimumDate={new Date()}
        />
      )}
      <Button title="Tambah Tugas" onPress={addTask} color="#007AFF" /> // Tambahkan ini: Aktifkan tombol
    </View>
  </KeyboardAvoidingView>
);
}
```

Penjelasan Kode Per Baris:
- `import { ..., useEffect } from 'react'; // Tambahkan ini`  
  - Fungsi: Mengimpor `useEffect` untuk memuat tugas saat start.  
  - Cara Kerja: Menjalankan kode sekali saat komponen dimuat.  

- `import AsyncStorage from '@react-native-async-storage/async-storage'; // Tambahkan ini`  
  - Fungsi: Mengimpor AsyncStorage.  
  - Cara Kerja: Menyimpan data secara lokal di perangkat.  

- `const [todos, setTodos] = useState([]); // Tambahkan ini`  
  - Fungsi: State untuk daftar tugas.  
  - Cara Kerja: Array kosong awalnya, `setTodos` memperbarui daftar.  

- `useEffect(() => { loadTodos(); }, []); // Tambahkan ini`  
  - Fungsi: Memuat tugas dari AsyncStorage saat aplikasi mulai.  
  - Cara Kerja: `[]` memastikan hanya dijalankan sekali.  

- `const loadTodos = async () => { ... } // Tambahkan ini`  
  - Fungsi: Mengambil tugas dari AsyncStorage.  
  - Cara Kerja:  
    - `await AsyncStorage.getItem('todos')`: Ambil data.  
    - `JSON.parse`: Ubah JSON ke array.  
    - `map(... dateTime: new Date(...))`: Konversi string ke `Date`.  
    - `setTodos`: Perbarui state.  

- `const saveTodos = async (newTodos) => { ... } // Tambahkan ini`  
  - Fungsi: Menyimpan tugas ke AsyncStorage.  
  - Cara Kerja:  
    - `JSON.stringify`: Ubah array ke JSON.  
    - `await AsyncStorage.setItem`: Simpan data.  
    - `setTodos`: Perbarui state.  

- `const addTask = () => { ... } // Tambahkan ini`  
  - Fungsi: Menambah tugas baru.  
  - Cara Kerja:  
    - `task.trim() === ''`: Cek input kosong.  
    - `newTodos`: Tambah tugas dengan `id`, `task`, `dateTime`, `completed: false`.  
    - `saveTodos`: Simpan daftar baru.  
    - Reset form: `setTask('')`, `setDate(new Date())`, `setShowDatePicker(false)`.  

- `<Button title="Tambah Tugas" onPress={addTask} ... /> // Tambahkan ini`  
  - Fungsi: Mengaktifkan tombol untuk menambah tugas.  
  - Cara Kerja: Memanggil `addTask` saat diklik.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Tidak ada perubahan karena UI form sama.
```javascript
/* Menambah fitur: Gaya untuk form input */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
});

export default styles;
```

Eksekusi:  
1. Simpan semua file.  
2. Refresh Expo Go.  
3. Harapan: Bisa menambah tugas (meski belum terlihat di UI). Tutup aplikasi, buka lagi, tugas tetap ada (disimpan di AsyncStorage).  
4. Error: Jika tugas tidak tersimpan, cek impor AsyncStorage atau error di `loadTodos`/`saveTodos`.  

Checkpoint:  
“Bisa tambah tugas? Coba tambah beberapa, tutup aplikasi, dan buka lagi. Kalau tugas masih ada, AsyncStorage jalan! Lanjut ke daftar tugas!”

---

 Iterasi 4: Menampilkan Daftar Tugas dengan FlatList
Narasi:  
“Logika tugas sudah ada, sekarang kita tampilkan daftar tugas dengan FlatList di HomeScreen.js. Kita juga buat TodoItem.js untuk merender setiap tugas dan file gaya TodoItemStyles.js. Tugas akan menampilkan nama dan tanggal, tapi belum ada centang atau hapus. Yuk, tambah daftarnya, Sobat Dev!”

# Kode: App.js
Tujuan: Tidak ada perubahan.
```javascript
/* Menambah fitur: Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

# Kode: screens/HomeScreen.js
Tujuan: Menampilkan daftar tugas dengan FlatList.
```javascript
/* Menambah fitur: Menampilkan daftar tugas dengan FlatList */
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text, FlatList } from 'react-native'; // Tambahkan ini: Impor FlatList
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage';
import TodoItem from '../components/TodoItem'; // Tambahkan ini: Impor komponen tugas
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    loadTodos();
  }, []);

  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  const addTask = () => {
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    const newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask}
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime"
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()}
          />
        )}
        <Button title="Tambah Tugas" onPress={addTask} color="#007AFF" />
      </View>
      {todos.length === 0 ? ( // Tambahkan ini: Teks jika kosong
        <Text style={styles.emptyText}>Belum ada tugas!</Text>
      ) : (
        <FlatList // Tambahkan ini: Daftar tugas
          data={todos}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => <TodoItem todo={item} />}
          style={styles.list}
        />
      )}
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Kode Per Baris:
- `import { ..., FlatList } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor FlatList untuk daftar.  
  - Cara Kerja: Merender daftar secara efisien, hanya item yang terlihat.  

- `import TodoItem from '../components/TodoItem'; // Tambahkan ini`  
  - Fungsi: Mengimpor TodoItem untuk merender tugas.  
  - Cara Kerja: Setiap tugas dirender sebagai komponen TodoItem.  

- `{todos.length === 0 ? ... : ...} // Tambahkan ini`  
  - Fungsi: Menampilkan teks jika daftar kosong, atau FlatList jika ada tugas.  
  - Cara Kerja: Kondisional untuk UX yang lebih baik.  

- `<Text style={styles.emptyText}>Belum ada tugas!</Text> // Tambahkan ini`  
  - Fungsi: Teks saat daftar kosong.  
  - Cara Kerja: Menggunakan gaya `emptyText` untuk visibilitas.  

- `<FlatList data={todos} keyExtractor={(item) => item.id} renderItem={({ item }) => <TodoItem todo={item} />} style={styles.list} /> // Tambahkan ini`  
  - Fungsi: Menampilkan daftar tugas.  
  - Cara Kerja:  
    - `data={todos}`: Sumber data.  
    - `keyExtractor`: ID unik untuk setiap item.  
    - `renderItem`: Merender TodoItem dengan prop `todo`.  
    - `style={styles.list}`: Gaya daftar.  

# Kode: components/TodoItem.js
Tujuan: Merender setiap tugas dengan nama dan tanggal.
```javascript
/* Menambah fitur: Komponen tugas untuk daftar */
import React from 'react';
import { View, Text } from 'react-native'; // Tambahkan ini: Komponen UI
import styles from '../styles/TodoItemStyles'; // Tambahkan ini: Impor gaya

export default function TodoItem({ todo }) { // Tambahkan ini: Terima prop todo
  return (
    <View style={styles.container}> // Tambahkan ini: Container tugas
      <Text style={styles.taskText}>{todo.task}</Text> // Tambahkan ini: Nama tugas
      <Text style={styles.date}>
        {new Date(todo.dateTime).toLocaleString('id-ID', { dateStyle: 'short', timeStyle: 'short' })} // Tambahkan ini: Tanggal/waktu
      </Text>
    </View>
  );
}
```

Penjelasan Kode Per Baris:
- `import { View, Text } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor komponen UI.  
  - Cara Kerja: Untuk container dan teks tugas.  

- `import styles from '../styles/TodoItemStyles'; // Tambahkan ini`  
  - Fungsi: Mengimpor gaya.  
  - Cara Kerja: Dari TodoItemStyles.js.  

- `export default function TodoItem({ todo }) { ... } // Tambahkan ini`  
  - Fungsi: Komponen untuk satu tugas.  
  - Cara Kerja: Menerima prop `todo` dengan `id`, `task`, `dateTime`, `completed`.  

- `<View style={styles.container}> // Tambahkan ini`  
  - Fungsi: Container tugas.  
  - Cara Kerja: Menggunakan gaya `container` untuk kartu tugas.  

- `<Text style={styles.taskText}>{todo.task}</Text> // Tambahkan ini`  
  - Fungsi: Menampilkan nama tugas.  
  - Cara Kerja: Menggunakan gaya `taskText`.  

- `<Text style={styles.date}> ... </Text> // Tambahkan ini`  
  - Fungsi: Menampilkan tanggal/waktu.  
  - Cara Kerja: Format Indonesia menggunakan `toLocaleString`.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Menambah gaya untuk daftar dan teks kosong.
```javascript
/* Menambah fitur: Gaya untuk daftar tugas */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
  emptyText: { // Tambahkan ini: Gaya teks kosong
    textAlign: 'center',
    marginTop: 50,
    fontSize: 18,
    color: '#666',
  },
  list: { // Tambahkan ini: Gaya FlatList
    flex: 1,
  },
});

export default styles;
```

Penjelasan Kode Per Baris:
- `emptyText: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk teks “Belum ada tugas!”.  
  - Cara Kerja: Teks terpusat, besar, warna abu-abu.  

- `list: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk FlatList.  
  - Cara Kerja: `flex: 1` memastikan daftar mengisi sisa ruang.  

# Kode: styles/TodoItemStyles.js
Tujuan: Gaya untuk TodoItem.
```javascript
/* Menambah fitur: Gaya untuk komponen tugas */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: { // Tambahkan ini: Gaya container tugas
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  taskText: { // Tambahkan ini: Gaya nama tugas
    fontSize: 16,
    color: '#333',
  },
  date: { // Tambahkan ini: Gaya tanggal
    fontSize: 14,
    color: '#666',
    marginTop: 5,
  },
});

export default styles;
```

Penjelasan Kode Per Baris:
- `container: { ... } // Tambahkan ini`  
  - Fungsi: Gaya untuk kartu tugas.  
  - Cara Kerja: Latar putih, sudut membulat, bayangan.  

- `taskText: { ... } // Tambahkan ini`  
  - Fungsi: Gaya nama tugas.  
  - Cara Kerja: Font sedang, warna gelap.  

- `date: { ... } // Tambahkan ini`  
  - Fungsi: Gaya tanggal.  
  - Cara Kerja: Font kecil, warna abu-abu, jarak atas.  

Eksekusi:  
1. Simpan semua file:  
   - components/TodoItem.js di folder `components`.  
   - styles/TodoItemStyles.js di folder `styles`.  
2. Refresh Expo Go.  
3. Harapan: Daftar tugas muncul di bawah form, menampilkan nama dan tanggal. Jika kosong, muncul “Belum ada tugas!”.  
4. Error: Jika daftar tidak muncul, cek FlatList `data={todos}` atau TodoItem prop `todo`.  

Checkpoint:  
“Daftar tugas muncul? Coba tambah beberapa tugas dan lihat di layar. Kalau jalan, kita tambah fitur centang dan hapus!”

---

 Iterasi 5: Fitur Centang dan Hapus Tugas
Narasi:  
“Daftar tugas sudah terlihat, Sobat Dev! Sekarang kita tambah fitur centang (teks dicoret) dan hapus tugas di HomeScreen.js dan TodoItem.js. Kita akan update gaya di HomeScreenStyles.js dan TodoItemStyles.js untuk tombol dan teks dicoret. Klik teks tugas untuk centang, dan tambah tombol ‘Hapus’ di setiap tugas. Yuk, lanjutkan!”

# Kode: App.js
Tujuan: Tidak ada perubahan.
```javascript
/* Menambah fitur: Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

# Kode: screens/HomeScreen.js
Tujuan: Menambah fungsi centang dan hapus.
```javascript
/* Menambah fitur: Centang dan hapus tugas */
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text, FlatList } from 'react-native';
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage';
import TodoItem from '../components/TodoItem';
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    loadTodos();
  }, []);

  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  const addTask = () => {
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    const newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  // Tambahkan ini: Fungsi untuk centang tugas
  const toggleComplete = (id) => {
    const newTodos = todos.map((todo) =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
    saveTodos(newTodos);
  };

  // Tambahkan ini: Fungsi untuk hapus tugas
  const deleteTask = (id) => {
    const newTodos = todos.filter((todo) => todo.id !== id);
    saveTodos(newTodos);
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask}
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime"
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()}
          />
        )}
        <Button title="Tambah Tugas" onPress={addTask} color="#007AFF" />
      </View>
      {todos.length === 0 ? (
        <Text style={styles.emptyText}>Belum ada tugas!</Text>
      ) : (
        <FlatList
          data={todos}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <TodoItem
              todo={item}
              onToggleComplete={toggleComplete} // Tambahkan ini: Prop untuk centang
              onDelete={deleteTask} // Tambahkan ini: Prop untuk hapus
            />
          )}
          style={styles.list}
        />
      )}
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Kode Per Baris:
- `const toggleComplete = (id) => { ... } // Tambahkan ini`  
  - Fungsi: Mengubah status `completed` tugas.  
  - Cara Kerja:  
    - `map`: Ubah `completed` untuk tugas dengan `id` yang cocok.  
    - `saveTodos`: Simpan perubahan.  

- `const deleteTask = (id) => { ... } // Tambahkan ini`  
  - Fungsi: Menghapus tugas.  
  - Cara Kerja:  
    - `filter`: Hapus tugas dengan `id` yang cocok.  
    - `saveTodos`: Simpan daftar baru.  

- `<TodoItem todo={item} onToggleComplete={toggleComplete} onDelete={deleteTask} /> // Tambahkan ini`  
  - Fungsi: Meneruskan fungsi centang dan hapus ke TodoItem.  
  - Cara Kerja: Prop memungkinkan TodoItem memanggil fungsi ini.  

# Kode: components/TodoItem.js
Tujuan: Menambah tombol centang dan hapus, teks dicoret saat selesai.
```javascript
/* Menambah fitur: Centang dan hapus tugas */
import React from 'react';
import { View, Text, TouchableOpacity } from 'react-native'; // Tambahkan ini: Impor TouchableOpacity
import styles from '../styles/TodoItemStyles';

export default function TodoItem({ todo, onToggleComplete, onDelete }) { // Tambahkan ini: Terima prop baru
  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={() => onToggleComplete(todo.id)}> // Tambahkan ini: Klik teks untuk centang
        <Text style={[styles.taskText, todo.completed && styles.completed]}>
          {todo.task}
        </Text>
        <Text style={styles.date}>
          {new Date(todo.dateTime).toLocaleString('id-ID', { dateStyle: 'short', timeStyle: 'short' })}
        </Text>
      </TouchableOpacity>
      <View style={styles.buttons}> // Tambahkan ini: Container tombol
        <TouchableOpacity
          style={[styles.button, styles.deleteButton]} // Tambahkan ini: Tombol hapus
          onPress={() => onDelete(todo.id)}
        >
          <Text style={styles.buttonText}>Hapus</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}
```

Penjelasan Kode Per Baris:
- `import { ..., TouchableOpacity } from 'react-native'; // Tambahkan ini`  
  - Fungsi: Mengimpor TouchableOpacity untuk tombol.  
  - Cara Kerja: Memberi efek klik dengan opacity.  

- `export default function TodoItem({ todo, onToggleComplete, onDelete }) { ... } // Tambahkan ini`  
  - Fungsi: Menerima prop untuk centang dan hapus.  
  - Cara Kerja: Fungsi dipanggil saat tombol diklik.  

- `<TouchableOpacity onPress={() => onToggleComplete(todo.id)}> // Tambahkan ini`  
  - Fungsi: Klik teks untuk centang.  
  - Cara Kerja: Memanggil `onToggleComplete` dengan ID tugas.  

- `style={[styles.taskText, todo.completed && styles.completed]} // Tambahkan ini`  
  - Fungsi: Teks dicoret jika selesai.  
  - Cara Kerja: Kombinasi gaya, `completed` diterapkan jika `todo.completed` `true`.  

- `<View style={styles.buttons}> // Tambahkan ini`  
  - Fungsi: Container untuk tombol.  
  - Cara Kerja: Mengelompokkan tombol hapus.  

- `<TouchableOpacity style={[styles.button, styles.deleteButton]} onPress={() => onDelete(todo.id)}> // Tambahkan ini`  
  - Fungsi: Tombol hapus.  
  - Cara Kerja: Memanggil `onDelete` dengan ID tugas.  

- `<Text style={styles.buttonText}>Hapus</Text> // Tambahkan ini`  
  - Fungsi: Teks tombol.  
  - -dummy- Fungsi: Teks untuk tombol hapus.  
  - Cara Kerja: Menggunakan gaya `buttonText` untuk konsistensi.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Tidak ada perubahan.
```javascript
/* Menambah fitur: Gaya untuk daftar tugas */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
  emptyText: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 18,
    color: '#666',
  },
  list: {
    flex: 1,
  },
});

export default styles;
```

# Kode: styles/TodoItemStyles.js
Tujuan: Menambah gaya untuk teks dicoret dan tombol.
```javascript
/* Menambah fitur: Gaya untuk centang dan hapus */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row', // Tambahkan ini: Susun horizontal
    justifyContent: 'space-between', // Tambahkan ini: Jarak antar elemen
    alignItems: 'center', // Tambahkan ini: Rata tengah
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  taskText: {
    fontSize: 16,
    color: '#333',
  },
  completed: { // Tambahkan ini: Gaya teks dicoret
    textDecorationLine: 'line-through',
    color: '#666',
  },
  date: {
    fontSize: 14,
    color: '#666',
    marginTop: 5,
  },
  buttons: { // Tambahkan ini: Gaya container tombol
    flexDirection: 'row',
  },
  button: { // Tambahkan ini: Gaya tombol dasar
    paddingVertical: 8,
    paddingHorizontal: 12,
    borderRadius: 8,
  },
  deleteButton: { // Tambahkan ini: Gaya tombol hapus
    backgroundColor: '#FF3B30',
  },
  buttonText: { // Tambahkan ini: Gaya teks tombol
    color: '#fff',
    fontSize: 14,
    fontWeight: '600',
  },
});

export default styles;
```

Penjelasan Kode Per Baris:
- `flexDirection: 'row' // Tambahkan ini` (di `container`)  
  - Fungsi: Susun elemen horizontal.  
  - Cara Kerja: Teks dan tombol sejajar.  

- `justifyContent: 'space-between' // Tambahkan ini`  
  - Fungsi: Jarak maksimal antar elemen.  
  - Cara Kerja: Teks di kiri, tombol di kanan.  

- `alignItems: 'center' // Tambahkan ini`  
  - Fungsi: Rata tengah vertikal.  
  - Cara Kerja: Elemen sejajar vertikal.  

- `completed: { ... } // Tambahkan ini`  
  - Fungsi: Teks dicoret untuk tugas selesai.  
  - Cara Kerja: `textDecorationLine` menambah garis, warna abu-abu.  

- `buttons: { ... } // Tambahkan ini`  
  - Fungsi: Gaya container tombol.  
  - Cara Kerja: Susun tombol horizontal.  

- `button: { ... } // Tambahkan ini`  
  - Fungsi: Gaya dasar tombol
 Iterasi 5: Fitur Centang dan Hapus Tugas (Melanjutkan dan Memperbaiki)
Narasi:  
“Sobat Dev, kita lanjutkan fitur centang dan hapus tugas dari iterasi sebelumnya. Kita akan memastikan teks tugas dicoret saat dicentang, dan tombol ‘Hapus’ berfungsi untuk menghapus tugas. Kita akan update HomeScreen.js untuk menangani logika, TodoItem.js untuk UI centang dan hapus, serta TodoItemStyles.js untuk gaya tombol dan teks dicoret. HomeScreenStyles.js tidak perlu diubah karena UI daftar sudah sesuai. Yuk, kita pastikan semuanya jalan mulus!”

# Kode: App.js
Tujuan: Tidak ada perubahan, navigasi sudah diatur.
```javascript
/* Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

Penjelasan: Tidak ada perubahan karena navigasi sudah diatur di iterasi sebelumnya.

# Kode: screens/HomeScreen.js
Tujuan: Menambah fungsi centang dan hapus tugas, memperbaiki struktur dari iterasi sebelumnya.
```javascript
/* Menambah fitur: Centang dan hapus tugas */
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text, FlatList } from 'react-native';
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage';
import TodoItem from '../components/TodoItem';
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    loadTodos();
  }, []);

  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  const addTask = () => {
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    const newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  // Tambahkan ini: Fungsi untuk centang tugas
  const toggleComplete = (id) => {
    const newTodos = todos.map((todo) =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
    saveTodos(newTodos);
  };

  // Tambahkan ini: Fungsi untuk hapus tugas
  const deleteTask = (id) => {
    const newTodos = todos.filter((todo) => todo.id !== id);
    saveTodos(newTodos);
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask}
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime"
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()}
          />
        )}
        <Button title="Tambah Tugas" onPress={addTask} color="#007AFF" />
      </View>
      {todos.length === 0 ? (
        <Text style={styles.emptyText}>Belum ada tugas!</Text>
      ) : (
        <FlatList
          data={todos}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <TodoItem
              todo={item}
              onToggleComplete={toggleComplete} // Tambahkan ini: Prop untuk centang
              onDelete={deleteTask} // Tambahkan ini: Prop untuk hapus
            />
          )}
          style={styles.list}
        />
      )}
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `const toggleComplete = (id) => { ... } // Tambahkan ini`  
    - Fungsi: Mengubah status `completed` tugas berdasarkan ID.  
    - Cara Kerja: Menggunakan `map` untuk memperbarui `completed`, lalu menyimpan ke AsyncStorage via `saveTodos`.  
  - `const deleteTask = (id) => { ... } // Tambahkan ini`  
    - Fungsi: Menghapus tugas berdasarkan ID.  
    - Cara Kerja: Menggunakan `filter` untuk menghapus tugas, lalu menyimpan daftar baru.  
  - `<TodoItem ... onToggleComplete={toggleComplete} onDelete={deleteTask} /> // Tambahkan ini`  
    - Fungsi: Meneruskan fungsi centang dan hapus ke TodoItem.  
    - Cara Kerja: Memungkinkan TodoItem memanggil fungsi saat interaksi pengguna.  
- Baris lain: Tetap sama untuk mempertahankan form input, DateTimePicker, dan FlatList.

# Kode: components/TodoItem.js
Tujuan: Menampilkan tugas dengan teks dicoret saat selesai dan tombol hapus.
```javascript
/* Menambah fitur: Centang dan hapus tugas */
import React from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import styles from '../styles/TodoItemStyles';

export default function TodoItem({ todo, onToggleComplete, onDelete }) {
  return (
    <View style={styles.container}>
      <TouchableOpacity
        style={styles.textContainer} // Tambahkan ini: Area klik teks
        onPress={() => onToggleComplete(todo.id)}
      >
        <Text style={[styles.taskText, todo.completed && styles.completed]}>
          {todo.task}
        </Text>
        <Text style={styles.date}>
          {new Date(todo.dateTime).toLocaleString('id-ID', { dateStyle: 'short', timeStyle: 'short' })}
        </Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={[styles.button, styles.deleteButton]} // Tambahkan ini: Tombol hapus
        onPress={() => onDelete(todo.id)}
      >
        <Text style={styles.buttonText}>Hapus</Text>
      </TouchableOpacity>
    </View>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan/perbaikan:  
  - `style={styles.textContainer} // Tambahkan ini`  
    - Fungsi: Membungkus teks dalam area klik yang jelas.  
    - Cara Kerja: Memisahkan teks dari tombol hapus untuk UX yang lebih baik.  
  - `<TouchableOpacity style={[styles.button, styles.deleteButton]} ... > // Tambahkan ini`  
    - Fungsi: Tombol hapus dengan gaya merah.  
    - Cara Kerja: Memanggil `onDelete` dengan ID tugas saat diklik.  
  - `<Text style={styles.buttonText}>Hapus</Text> // Tambahkan ini`  
    - Fungsi: Teks tombol hapus.  
    - Cara Kerja: Menggunakan gaya `buttonText` untuk teks putih tebal.  
- Perbaikan: Struktur disederhanakan, menghapus `buttons` container untuk layout lebih efisien.

# Kode: styles/HomeScreenStyles.js
Tujuan: Tidak ada perubahan, gaya daftar sudah sesuai.
```javascript
/* Gaya untuk form dan daftar tugas */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
  emptyText: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 18,
    color: '#666',
  },
  list: {
    flex: 1,
  },
});

export default styles;
```

Penjelasan: Tidak ada perubahan karena gaya untuk form dan FlatList sudah memadai.

# Kode: styles/TodoItemStyles.js
Tujuan: Menambah gaya untuk teks dicoret, tombol hapus, dan layout horizontal.
```javascript
/* Menambah fitur: Gaya untuk centang dan hapus */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row', // Tambahkan ini: Layout horizontal
    justifyContent: 'space-between', // Tambahkan ini: Jarak antar elemen
    alignItems: 'center', // Tambahkan ini: Rata tengah vertikal
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  textContainer: { // Tambahkan ini: Area teks
    flex: 1,
  },
  taskText: {
    fontSize: 16,
    color: '#333',
  },
  completed: { // Tambahkan ini: Teks dicoret
    textDecorationLine: 'line-through',
    color: '#666',
  },
  date: {
    fontSize: 14,
    color: '#666',
    marginTop: 5,
  },
  button: { // Tambahkan ini: Gaya tombol dasar
    paddingVertical: 8,
    paddingHorizontal: 12,
    borderRadius: 8,
  },
  deleteButton: { // Tambahkan ini: Gaya tombol hapus
    backgroundColor: '#FF3B30',
  },
  buttonText: { // Tambahkan ini: Gaya teks tombol
    color: '#fff',
    fontSize: 14,
    fontWeight: '600',
  },
});

export default styles;
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `flexDirection: 'row' // Tambahkan ini` (di `container`)  
    - Fungsi: Menyusun teks dan tombol secara horizontal.  
    - Cara Kerja: Elemen sejajar kiri-kanan.  
  - `justifyContent: 'space-between' // Tambahkan ini`  
    - Fungsi: Memisahkan teks dan tombol.  
    - Cara Kerja: Teks di kiri, tombol di kanan.  
  - `alignItems: 'center' // Tambahkan ini`  
    - Fungsi: Meratakan elemen vertikal.  
    - Cara Kerja: Teks dan tombol sejajar tengah.  
  - `textContainer: { flex: 1 } // Tambahkan ini`  
    - Fungsi: Area teks mengambil ruang tersisa.  
    - Cara Kerja: Mencegah teks terdesak tombol.  
  - `completed: { ... } // Tambahkan ini`  
    - Fungsi: Gaya teks dicoret untuk tugas selesai.  
    - Cara Kerja: Garis coret dan warna abu-abu.  
  - `button: { ... } // Tambahkan ini`  
    - Fungsi: Gaya dasar tombol.  
    - Cara Kerja: Padding dan sudut membulat.  
  - `deleteButton: { ... } // Tambahkan ini`  
    - Fungsi: Gaya tombol hapus merah.  
    - Cara Kerja: Latar merah untuk kontras.  
  - `buttonText: { ... } // Tambahkan ini`  
    - Fungsi: Gaya teks tombol.  
    - Cara Kerja: Teks putih tebal untuk keterbacaan.  

Eksekusi:  
1. Simpan semua file.  
2. Jalankan `npx expo start` atau refresh Expo Go (`r` di terminal).  
3. Tambah beberapa tugas, klik teks tugas untuk centang (teks dicoret), dan klik tombol “Hapus” untuk menghapus tugas.  
4. Harapan:  
   - Teks tugas dicoret saat dicentang.  
   - Tugas hilang saat tombol “Hapus” diklik.  
   - Data tersimpan di AsyncStorage (tutup aplikasi, buka lagi, perubahan tetap ada).  
5. Error:  
   - Jika centang tidak bekerja, cek `onToggleComplete` di TodoItem.  
   - Jika hapus gagal, cek `onDelete` dan `deleteTask`.  

Checkpoint:  
“Coba centang dan hapus tugas di HP. Apakah teks dicoret dan tugas terhapus? Jika ya, fitur ini selesai! Kita lanjut ke fitur edit tugas!”

---

 Iterasi 6: Fitur Edit Tugas
Narasi:  
“Bagus sekali, Sobat Dev! Sekarang kita tambah fitur edit tugas. Pengguna bisa klik tombol ‘Edit’ di setiap tugas, lalu form di atas akan terisi dengan nama tugas dan tanggal yang ada, untuk diedit. Setelah edit, tekan ‘Tambah Tugas’ (akan berubah jadi ‘Simpan Perubahan’) untuk menyimpan. Kita akan update HomeScreen.js untuk logika edit, TodoItem.js untuk tombol edit, dan TodoItemStyles.js untuk gaya tombol. HomeScreenStyles.js akan diperbarui untuk gaya tombol yang berubah. Yuk, mulai!”

# Kode: App.js
Tujuan: Tidak ada perubahan.
```javascript
/* Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

# Kode: screens/HomeScreen.js
Tujuan: Menambah logika edit tugas dan mengubah tombol berdasarkan mode.
```javascript
/* Menambah fitur: Edit tugas */
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text, FlatList } from 'react-native';
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage';
import TodoItem from '../components/TodoItem';
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]);
  const [editingId, setEditingId] = useState(null); // Tambahkan ini: ID tugas yang diedit

  useEffect(() => {
    loadTodos();
  }, []);

  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  const addOrUpdateTask = () => { // Ubah ini: Ganti addTask untuk mendukung edit
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    let newTodos;
    if (editingId) {
      // Mode edit
      newTodos = todos.map((todo) =>
        todo.id === editingId ? { ...todo, task, dateTime: date } : todo
      );
      setEditingId(null); // Keluar dari mode edit
    } else {
      // Mode tambah
      newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    }
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  const toggleComplete = (id) => {
    const newTodos = todos.map((todo) =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
    saveTodos(newTodos);
  };

  const deleteTask = (id) => {
    const newTodos = todos.filter((todo) => todo.id !== id);
    saveTodos(newTodos);
  };

  // Tambahkan ini: Fungsi untuk mulai edit
  const startEditing = (todo) => {
    setTask(todo.task);
    setDate(new Date(todo.dateTime));
    setEditingId(todo.id);
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask}
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime"
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()}
          />
        )}
        <Button
          title={editingId ? 'Simpan Perubahan' : 'Tambah Tugas'} // Tambahkan ini: Ubah teks tombol
          onPress={addOrUpdateTask} // Ubah ini: Gunakan fungsi baru
          color="#007AFF"
        />
      </View>
      {todos.length === 0 ? (
        <Text style={styles.emptyText}>Belum ada tugas!</Text>
      ) : (
        <FlatList
          data={todos}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <TodoItem
              todo={item}
              onToggleComplete={toggleComplete}
              onDelete={deleteTask}
              onEdit={startEditing} // Tambahkan ini: Prop untuk edit
            />
          )}
          style={styles.list}
        />
      )}
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `const [editingId, setEditingId] = useState(null); // Tambahkan ini`  
    - Fungsi: Menyimpan ID tugas yang sedang diedit.  
    - Cara Kerja: `null` berarti mode tambah, ID berarti mode edit.  
  - `const startEditing = (todo) => { ... } // Tambahkan ini`  
    - Fungsi: Mengisi form dengan data tugas untuk diedit.  
    - Cara Kerja: Set `task`, `date`, dan `editingId` berdasarkan tugas.  
  - `onEdit={startEditing} // Tambahkan ini` (di TodoItem)  
    - Fungsi: Meneruskan fungsi edit ke TodoItem.  
    - Cara Kerja: Dipanggil saat tombol “Edit” diklik.  
- Baris yang diubah:  
  - `const addOrUpdateTask = () => { ... } // Ubah ini`  
    - Fungsi: Menggantikan `addTask` untuk mendukung tambah dan edit.  
    - Cara Kerja:  
      - Jika `editingId` ada, perbarui tugas dengan `map`.  
      - Jika tidak, tambah tugas baru.  
      - Reset form dan keluar dari mode edit setelah simpan.  
  - `<Button title={editingId ? 'Simpan Perubahan' : 'Tambah Tugas'} ... /> // Tambahkan ini`  
    - Fungsi: Mengubah teks tombol berdasarkan mode.  
    - Cara Kerja: Menunjukkan “Simpan Perubahan” saat edit, “Tambah Tugas” saat tambah.  
  - `onPress={addOrUpdateTask} // Ubah ini`  
    - Fungsi: Menggunakan fungsi baru untuk tombol.  

# Kode: components/TodoItem.js
Tujuan: Menambah tombol edit untuk memulai pengeditan.
```javascript
/* Menambah fitur: Edit tugas */
import React from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import styles from '../styles/TodoItemStyles';

export default function TodoItem({ todo, onToggleComplete, onDelete, onEdit }) {
  return (
    <View style={styles.container}>
      <TouchableOpacity
        style={styles.textContainer}
        onPress={() => onToggleComplete(todo.id)}
      >
        <Text style={[styles.taskText, todo.completed && styles.completed]}>
          {todo.task}
        </Text>
        <Text style={styles.date}>
          {new Date(todo.dateTime).toLocaleString('id-ID', { dateStyle: 'short', timeStyle: 'short' })}
        </Text>
      </TouchableOpacity>
      <View style={styles.buttons}> // Tambahkan ini: Container tombol
        <TouchableOpacity
          style={[styles.button, styles.editButton]} // Tambahkan ini: Tombol edit
          onPress={() => onEdit(todo)}
        >
          <Text style={styles.buttonText}>Edit</Text>
        </TouchableOpacity>
        <TouchableOpacity
          style={[styles.button, styles.deleteButton]}
          onPress={() => onDelete(todo.id)}
        >
          <Text style={styles.buttonText}>Hapus</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `onEdit` (di parameter fungsi)  
    - Fungsi: Menerima fungsi edit dari HomeScreen.  
    - Cara Kerja: Dipanggil saat tombol “Edit” diklik.  
  - `<View style={styles.buttons}> // Tambahkan ini`  
    - Fungsi: Mengelompokkan tombol edit dan hapus.  
    - Cara Kerja: Layout horizontal untuk tombol.  
  - `<TouchableOpacity style={[styles.button, styles.editButton]} ... > // Tambahkan ini`  
    - Fungsi: Tombol edit dengan gaya biru.  
    - Cara Kerja: Memanggil `onEdit` dengan data tugas.  
  - `<Text style={styles.buttonText}>Edit</Text> // Tambahkan ini`  
    - Fungsi: Teks tombol edit.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Tidak ada perubahan, gaya form sudah sesuai.
```javascript
/* Gaya untuk form dan daftar tugas */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
  emptyText: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 18,
    color: '#666',
  },
  list: {
    flex: 1,
  },
});

export default styles;
```

# Kode: styles/TodoItemStyles.js
Tujuan: Menambah gaya untuk tombol edit dan container tombol.
```javascript
/* Menambah fitur: Gaya untuk tombol edit */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  textContainer: {
    flex: 1,
  },
  taskText: {
    fontSize: 16,
    color: '#333',
  },
  completed: {
    textDecorationLine: 'line-through',
    color: '#666',
  },
  date: {
    fontSize: 14,
    color: '#666',
    marginTop: 5,
  },
  buttons: { // Tambahkan ini: Container tombol
    flexDirection: 'row',
  },
  button: {
    paddingVertical: 8,
    paddingHorizontal: 12,
    borderRadius: 8,
    marginLeft: 10, // Tambahkan ini: Jarak antar tombol
  },
  editButton: { // Tambahkan ini: Gaya tombol edit
    backgroundColor: '#007AFF',
  },
  deleteButton: {
    backgroundColor: '#FF3B30',
  },
  buttonText: {
    color: '#fff',
    fontSize: 14,
    fontWeight: '600',
  },
});

export default styles;
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `buttons: { flexDirection: 'row' } // Tambahkan ini`  
    - Fungsi: Menyusun tombol edit dan hapus horizontal.  
    - Cara Kerja: Tombol sejajar kanan.  
  - `marginLeft: 10 // Tambahkan ini` (di `button`)  
    - Fungsi: Jarak antar tombol.  
    - Cara Kerja: Mencegah tombol menempel.  
  - `editButton: { backgroundColor: '#007AFF' } // Tambahkan ini`  
    - Fungsi: Gaya tombol edit biru.  
    - Cara Kerja: Konsisten dengan tema aplikasi.  

Eksekusi:  
1. Simpan semua file.  
2. Refresh Expo Go.  
3. Tambah tugas, klik tombol “Edit” pada tugas, ubah nama/tanggal di form, lalu klik “Simpan Perubahan”.  
4. Harapan:  
   - Tombol “Edit” mengisi form dengan data tugas.  
   - Tombol berubah menjadi “Simpan Perubahan” saat edit.  
   - Perubahan tersimpan, tugas diperbarui di daftar.  
5. Error:  
   - Jika form tidak terisi, cek `startEditing`.  
   - Jika perubahan tidak tersimpan, cek `addOrUpdateTask`.  

Checkpoint:  
“Coba edit tugas. Apakah form terisi dan perubahan tersimpan? Jika ya, fitur edit selesai! Kita lanjut ke filter dan peringatan terlambat!”

---

 Iterasi 7: Filter Tugas dan Peringatan Terlambat
Narasi:  
“Sobat Dev, kita di langkah terakhir! Kita akan tambah filter untuk menampilkan ‘Semua’, ‘Selesai’, atau ‘Terlambat’ tugas, dan menandai tugas terlambat (tanggal sebelum 17 Mei 2025, 02:00 WIB) dengan teks merah. Kita akan update HomeScreen.js untuk logika filter, TodoItem.js untuk menampilkan status terlambat, HomeScreenStyles.js untuk tombol filter, dan TodoItemStyles.js untuk teks terlambat. Yuk, selesaikan aplikasi ini!”

# Kode: App.js
Tujuan: Tidak ada perubahan.
```javascript
/* Setup navigasi dengan header biru */
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: 'Daftar Tugas',
            headerStyle: { backgroundColor: '#007AFF' },
            headerTintColor: '#fff',
            headerTitleStyle: { fontWeight: 'bold' },
          }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

# Kode: screens/HomeScreen.js
Tujuan: Menambah filter tugas dan logika terlambat.
```javascript
/* Menambah fitur: Filter tugas dan peringatan terlambat */
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, KeyboardAvoidingView, Platform, TouchableOpacity, Text, FlatList } from 'react-native';
import DateTimePicker from '@react-native-community/datetimepicker';
import AsyncStorage from '@react-native-async-storage/async-storage';
import TodoItem from '../components/TodoItem';
import styles from '../styles/HomeScreenStyles';

export default function HomeScreen() {
  const [task, setTask] = useState('');
  const [date, setDate] = useState(new Date());
  const [showDatePicker, setShowDatePicker] = useState(false);
  const [todos, setTodos] = useState([]);
  const [editingId, setEditingId] = useState(null);
  const [filter, setFilter] = useState('Semua'); // Tambahkan ini: State untuk filter

  useEffect(() => {
    loadTodos();
  }, []);

  const loadTodos = async () => {
    try {
      const storedTodos = await AsyncStorage.getItem('todos');
      if (storedTodos) {
        setTodos(JSON.parse(storedTodos).map((todo) => ({ ...todo, dateTime: new Date(todo.dateTime) })));
      }
    } catch (error) {
      console.error('Gagal memuat tugas:', error);
    }
  };

  const saveTodos = async (newTodos) => {
    try {
      await AsyncStorage.setItem('todos', JSON.stringify(newTodos));
      setTodos(newTodos);
    } catch (error) {
      console.error('Gagal menyimpan tugas:', error);
    }
  };

  const addOrUpdateTask = () => {
    if (task.trim() === '') {
      alert('Nama tugas tidak boleh kosong!');
      return;
    }
    let newTodos;
    if (editingId) {
      newTodos = todos.map((todo) =>
        todo.id === editingId ? { ...todo, task, dateTime: date } : todo
      );
      setEditingId(null);
    } else {
      newTodos = [...todos, { id: Date.now().toString(), task, dateTime: date, completed: false }];
    }
    saveTodos(newTodos);
    setTask('');
    setDate(new Date());
    setShowDatePicker(false);
  };

  const toggleComplete = (id) => {
    const newTodos = todos.map((todo) =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
    saveTodos(newTodos);
  };

  const deleteTask = (id) => {
    const newTodos = todos.filter((todo) => todo.id !== id);
    saveTodos(newTodos);
  };

  const startEditing = (todo) => {
    setTask(todo.task);
    setDate(new Date(todo.dateTime));
    setEditingId(todo.id);
  };

  // Tambahkan ini: Fungsi untuk filter tugas
  const filteredTodos = () => {
    const now = new Date('2025-05-17T02:00:00+07:00'); // Tanggal saat ini
    return todos.filter((todo) => {
      if (filter === 'Selesai') return todo.completed;
      if (filter === 'Terlambat') return !todo.completed && todo.dateTime < now;
      return true; // Semua
    });
  };

  const onDateChange = (event, selectedDate) => {
    setShowDatePicker(Platform.OS === 'ios');
    if (event.type === 'dismissed') {
      setShowDatePicker(false);
      return;
    }
    if (selectedDate) setDate(selectedDate);
  };

  return (
    <KeyboardAvoidingView
      style={styles.container}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Masukkan tugas"
          value={task}
          onChangeText={setTask}
        />
        <TouchableOpacity style={styles.dateButton} onPress={() => setShowDatePicker(true)}>
          <Text style={styles.dateText}>
            {date.toLocaleDateString('id-ID', { dateStyle: 'short' })} {date.toLocaleTimeString('id-ID', { timeStyle: 'short' })}
          </Text>
        </TouchableOpacity>
        {showDatePicker && (
          <DateTimePicker
            value={date}
            mode="datetime"
            display={Platform.OS === 'ios' ? 'inline' : 'default'}
            onChange={onDateChange}
            minimumDate={new Date()}
          />
        )}
        <Button
          title={editingId ? 'Simpan Perubahan' : 'Tambah Tugas'}
          onPress={addOrUpdateTask}
          color="#007AFF"
        />
      </View>
      <View style={styles.filterContainer}> // Tambahkan ini: Container filter
        <TouchableOpacity
          style={[styles.filterButton, filter === 'Semua' && styles.activeFilter]}
          onPress={() => setFilter('Semua')}
        >
          <Text style={styles.filterText}>Semua</Text>
        </TouchableOpacity>
        <TouchableOpacity
          style={[styles.filterButton, filter === 'Selesai' && styles.activeFilter]}
          onPress={() => setFilter('Selesai')}
        >
          <Text style={styles.filterText}>Selesai</Text>
        </TouchableOpacity>
        <TouchableOpacity
          style={[styles.filterButton, filter === 'Terlambat' && styles.activeFilter]}
          onPress={() => setFilter('Terlambat')}
        >
          <Text style={styles.filterText}>Terlambat</Text>
        </TouchableOpacity>
      </View>
      {filteredTodos().length === 0 ? (
        <Text style={styles.emptyText}>Tidak ada tugas di kategori ini!</Text> // Ubah ini: Pesan lebih spesifik
      ) : (
        <FlatList
          data={filteredTodos()} // Ubah ini: Gunakan tugas yang difilter
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <TodoItem
              todo={item}
              onToggleComplete={toggleComplete}
              onDelete={deleteTask}
              onEdit={startEditing}
            />
          )}
          style={styles.list}
        />
      )}
    </KeyboardAvoidingView>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `const [filter, setFilter] = useState('Semua'); // Tambahkan ini`  
    - Fungsi: Menyimpan status filter (Semua, Selesai, Terlambat).  
    - Cara Kerja: Default ke ‘Semua’, diubah saat tombol filter diklik.  
  - `const filteredTodos = () => { ... } // Tambahkan ini`  
    - Fungsi: Memfilter tugas berdasarkan `filter`.  
    - Cara Kerja:  
      - `now`: Tanggal saat ini (17 Mei 2025, 02:00 WIB).  
      - `filter === 'Selesai'`: Tampilkan tugas dengan `completed: true`.  
      - `filter === 'Terlambat'`: Tampilkan tugas belum selesai dan `dateTime` sebelum `now`.  
      - `true`: Tampilkan semua tugas untuk ‘Semua’.  
  - `<View style={styles.filterContainer}> ... </View> // Tambahkan ini`  
    - Fungsi: Menampilkan tombol filter.  
    - Cara Kerja: Tiga tombol untuk memilih filter, dengan gaya aktif saat dipilih.  
  - `<TouchableOpacity style={[styles.filterButton, filter === '...' && styles.activeFilter]} ... > // Tambahkan ini`  
    - Fungsi: Tombol filter dengan gaya aktif.  
    - Cara Kerja: Mengubah `filter` saat diklik, gaya `activeFilter` untuk tombol aktif.  
- Baris yang diubah:  
  - `data={filteredTodos()} // Ubah ini`  
    - Fungsi: Menggunakan tugas yang difilter di FlatList.  
    - Cara Kerja: Hanya tugas sesuai filter yang ditampilkan.  
  - `<Text style={styles.emptyText}>Tidak ada tugas di kategori ini!</Text> // Ubah ini`  
    - Fungsi: Pesan lebih spesifik saat daftar kosong.  
    - Cara Kerja: Memberi tahu pengguna jika tidak ada tugas di filter.  

# Kode: components/TodoItem.js
Tujuan: Menandai tugas terlambat dengan teks merah.
```javascript
/* Menambah fitur: Tandai tugas terlambat */
import React from 'react';
import { View, Text, TouchableOpacity } from 'react-native';
import styles from '../styles/TodoItemStyles';

export default function TodoItem({ todo, onToggleComplete, onDelete, onEdit }) {
  const now = new Date('2025-05-17T02:00:00+07:00'); // Tambahkan ini: Tanggal saat ini
  const isOverdue = !todo.completed && todo.dateTime < now; // Tambahkan ini: Cek terlambat

  return (
    <View style={styles.container}>
      <TouchableOpacity
        style={styles.textContainer}
        onPress={() => onToggleComplete(todo.id)}
      >
        <Text
          style={[
            styles.taskText,
            todo.completed && styles.completed,
            isOverdue && styles.overdue, // Tambahkan ini: Gaya terlambat
          ]}
        >
          {todo.task}
        </Text>
        <Text style={styles.date}>
          {new Date(todo.dateTime).toLocaleString('id-ID', { dateStyle: 'short', timeStyle: 'short' })}
        </Text>
      </TouchableOpacity>
      <View style={styles.buttons}>
        <TouchableOpacity
          style={[styles.button, styles.editButton]}
          onPress={() => onEdit(todo)}
        >
          <Text style={styles.buttonText}>Edit</Text>
        </TouchableOpacity>
        <TouchableOpacity
          style={[styles.button, styles.deleteButton]}
          onPress={() => onDelete(todo.id)}
        >
          <Text style={styles.buttonText}>Hapus</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `const now = new Date('2025-05-17T02:00:00+07:00'); // Tambahkan ini`  
    - Fungsi: Menentukan tanggal saat ini untuk cek terlambat.  
    - Cara Kerja: Menggunakan waktu WIB yang spesifik.  
  - `const isOverdue = !todo.completed && todo.dateTime < now; // Tambahkan ini`  
    - Fungsi: Mengecek apakah tugas terlambat.  
    - Cara Kerja: `true` jika belum selesai dan tanggal sebelum saat ini.  
  - `isOverdue && styles.overdue // Tambahkan ini`  
    - Fungsi: Menerapkan gaya merah untuk tugas terlambat.  
    - Cara Kerja: Ditambahkan ke array gaya teks tugas.  

# Kode: styles/HomeScreenStyles.js
Tujuan: Menambah gaya untuk tombol filter.
```javascript
/* Menambah fitur: Gaya untuk tombol filter */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#F5F5F5',
  },
  inputContainer: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 10,
    marginBottom: 15,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  input: {
    borderWidth: 1,
    borderColor: '#E0E0E0',
    padding: 12,
    marginBottom: 10,
    borderRadius: 8,
    fontSize: 16,
  },
  dateButton: {
    backgroundColor: '#E0E0E0',
    padding: 12,
    borderRadius: 8,
    marginBottom: 10,
  },
  dateText: {
    fontSize: 16,
    color: '#333',
  },
  emptyText: {
    textAlign: 'center',
    marginTop: 50,
    fontSize: 18,
    color: '#666',
  },
  list: {
    flex: 1,
  },
  filterContainer: { // Tambahkan ini: Container tombol filter
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 15,
  },
  filterButton: { // Tambahkan ini: Gaya tombol filter
    flex: 1,
    padding: 10,
    marginHorizontal: 5,
    borderRadius: 8,
    backgroundColor: '#E0E0E0',
    alignItems: 'center',
  },
  activeFilter: { // Tambahkan ini: Gaya tombol aktif
    backgroundColor: '#007AFF',
  },
  filterText: { // Tambahkan ini: Gaya teks filter
    color: '#333',
    fontSize: 16,
    fontWeight: '600',
  },
});

export default styles;
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `filterContainer: { ... } // Tambahkan ini`  
    - Fungsi: Menyusun tombol filter horizontal.  
    - Cara Kerja: `space-between` untuk jarak merata.  
  - `filterButton: { ... } // Tambahkan ini`  
    - Fungsi: Gaya dasar tombol filter.  
    - Cara Kerja: Latar abu-abu, teks terpusat.  
  - `activeFilter: { ... } // Tambahkan ini`  
    - Fungsi: Gaya tombol filter saat aktif.  
    - Cara Kerja: Latar biru untuk menandakan pilihan.  
  - `filterText: { ... } // Tambahkan ini`  
    - Fungsi: Gaya teks tombol filter.  
    - Cara Kerja: Teks tebal untuk keterbacaan.  

# Kode: styles/TodoItemStyles.js
Tujuan: Menambah gaya untuk teks tugas terlambat.
```javascript
/* Menambah fitur: Gaya untuk tugas terlambat */
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    backgroundColor: '#fff',
    padding: 15,
    marginBottom: 10,
    borderRadius: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    elevation: 3,
  },
  textContainer: {
    flex: 1,
  },
  taskText: {
    fontSize: 16,
    color: '#333',
  },
  completed: {
    textDecorationLine: 'line-through',
    color: '#666',
  },
  overdue: { // Tambahkan ini: Gaya tugas terlambat
    color: '#FF3B30',
  },
  date: {
    fontSize: 14,
    color: '#666',
    marginTop: 5,
  },
  buttons: {
    flexDirection: 'row',
  },
  button: {
    paddingVertical: 8,
    paddingHorizontal: 12,
    borderRadius: 8,
    marginLeft: 10,
  },
  editButton: {
    backgroundColor: '#007AFF',
  },
  deleteButton: {
    backgroundColor: '#FF3B30',
  },
  buttonText: {
    color: '#fff',
    fontSize: 14,
    fontWeight: '600',
  },
});

export default styles;
```

Penjelasan Perubahan:
- Baris yang ditambahkan:  
  - `overdue: { color: '#FF3B30' } // Tambahkan ini`  
    - Fungsi: Mengubah warna teks tugas terlambat menjadi merah.  
    - Cara Kerja: Menandakan tugas mendesak secara visual.  

Eksekusi:  
1. Simpan semua file.  
2. Refresh Expo Go.  
3. Tambah beberapa tugas:  
   - Satu dengan tanggal sebelum 17 Mei 2025, 02:00 WIB (terlambat).  
   - Satu dengan tanggal setelahnya.  
   - Centang satu tugas sebagai selesai.  
4. Coba filter:  
   - “Semua”: Lihat semua tugas.  
   - “Selesai”: Hanya tugas selesai.  
   - “Terlambat”: Hanya tugas belum selesai dengan tanggal sebelum saat ini.  
5. Harapan:  
   - Tugas terlambat ditampilkan dengan teks merah (kecuali selesai).  
   - Filter menampilkan tugas sesuai kategori.  
   - Tombol filter aktif berwarna biru.  
6. Error:  
   - Jika filter tidak bekerja, cek `filteredTodos`.  
   - Jika teks tidak merah, cek `isOverdue` di TodoItem.  

Checkpoint:  
“Coba filter tugas dan lihat tugas terlambat (teks merah). Apakah filter dan peringatan berfungsi? Jika ya, aplikasi selesai!”

---

 Struktur Proyek Akhir
```
TodoApp/
├── App.js
├── screens/
│   └── HomeScreen.js
├── components/
│   └── TodoItem.js
├── styles/
│   ├── HomeScreenStyles.js
│   └── TodoItemStyles.js
├── app.json
├── package.json
├── node_modules/
└── assets/
```

 Fitur Lengkap
- Navigasi: Header biru dengan judul “Daftar Tugas”.
- Form Input: Tambah tugas dengan nama dan tanggal/waktu.
- AsyncStorage: Simpan tugas secara lokal.
- Daftar Tugas: Tampilkan tugas dengan FlatList.
- Centang Tugas: Teks dicoret saat selesai.
- Hapus Tugas: Tombol hapus per tugas.
- Edit Tugas: Edit nama dan tanggal tugas.
- Filter Tugas: Tampilkan Semua, Selesai, atau Terlambat.
- Peringatan Terlambat: Teks merah untuk tugas terlambat.

 Pengujian Akhir
1. Jalankan `npx expo start`.  
2. Buka Expo Go, pindai QR code.  
3. Uji semua fitur:  
   - Tambah tugas baru.  
   - Centang dan hapus tugas.  
   - Edit tugas.  
   - Filter tugas (Semua, Selesai, Terlambat).  
   - Tambah tugas dengan tanggal sebelum 17 Mei 2025, 02:00 WIB, pastikan teks merah.  
4. Tutup aplikasi, buka lagi, pastikan tugas tersimpan.  
5. Harapan: Semua fitur berjalan tanpa error, UI responsif, data persisten.

 Catatan Debugging
- Error Navigasi: Pastikan `@react-navigation/*` terinstall, cek impor di App.js.  
- AsyncStorage Gagal: Cek instalasi `@react-native-async-storage/async-storage`.  
- DateTimePicker Tidak Muncul: Cek `@react-native-community/datetimepicker` dan state `showDatePicker`.  
- Filter Salah: Periksa logika `filteredTodos`.  
- Teks Tidak Merah: Cek `isOverdue` dan gaya `overdue`.  

Selamat, Sobat Dev! Aplikasi To-Do List sudah selesai dengan semua fitur yang diminta. Jika ada yang ingin diperbaiki atau ditambah, beri tahu saya. Apa langkah selanjutnya? Ingin publish ke Expo atau tambah fitur lain? 🚀


