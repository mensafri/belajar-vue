# Catatan Pembelajaran Vue.js

## Pendahuluan

Ini adalah catatan pembelajaran saya saat mempelajari Vue.js, dimulai dari langkah awal membuat proyek hingga mencoba fitur-fitur seperti data binding, event handling, dan penggunaan lifecycle hooks. Saya menggunakan `pnpm` untuk mengelola dependensi karena lebih cepat dan efisien.

---

## 1. Cara Membuat Proyek Vue.js

### Langkah-Langkah:

1. Pertama, saya menjalankan perintah berikut untuk membuat proyek baru:
   ```bash
   pnpm create vue@latest
   ```
2. Saya memilih beberapa opsi saat membuat proyek:
   - Nama proyek: **vue-belajar**.
   - Fitur: Saya memilih TypeScript, Vue Router, dan Pinia (untuk eksplorasi ke depan).
   - ESLint dan Prettier: Saya aktifkan agar kode lebih rapi.
3. Setelah itu, saya masuk ke folder proyek:
   ```bash
   cd vue-belajar
   ```
4. Jika dependensinya belum otomatis terinstal, saya menjalankan:
   ```bash
   pnpm install
   ```
5. Untuk menjalankan server lokal, saya gunakan:
   ```bash
   pnpm dev
   ```
6. Proyek saya bisa diakses di browser melalui `http://localhost:5173`.

---

## 2. Membuat Komponen Dasar: App2.vue

Saya mulai dengan membuat komponen sederhana untuk memahami cara kerja Vue.js, khususnya **data binding**, **event handling**, dan **conditional rendering**.

### Apa yang Saya Pelajari:

1. **Data Binding**: Menggunakan `{{ }}` untuk menampilkan data di template.
2. **Event Handling**: Menggunakan `@click` untuk menangani klik tombol.
3. **Conditional Rendering**: Menggunakan `v-if`, `v-else-if`, dan `v-else` untuk menampilkan elemen berdasarkan kondisi.

### Kode:

Berikut adalah kode yang saya buat di file `App2.vue`:

```vue
<script>
export default {
	data() {
		return {
			name: "Sapri",
			status: "active",
			tasks: ["Tugas 1", "Tugas 2", "Tugas 3"],
			link: "https://google.com",
		};
	},
	methods: {
		toggleStatus() {
			this.status = this.status === "active" ? "pending" : "active";
		},
	},
};
</script>

<template>
	<h1>{{ name }}</h1>
	<h1 v-if="status == 'active'">User is Active</h1>
	<h1 v-else-if="status == 'pending'">User is Pending</h1>
	<h1 v-else>User is Not Active</h1>

	<h3>Tugas:</h3>
	<ul>
		<li
			v-for="task in tasks"
			:key="task">
			{{ task }}
		</li>
	</ul>

	<a :href="link">Pergi ke Google</a>
	<button @click="toggleStatus">Ubah Status</button>
</template>
```

### Cara Saya Gunakan:

1. Saya simpan kode di file `App2.vue` di folder `src/components`.
2. Lalu, saya impor komponen ini ke dalam `App.vue`:

   ```vue
   <template>
   	<App2 />
   </template>

   <script>
   import App2 from "./components/App2.vue";

   export default {
   	components: {
   		App2,
   	},
   };
   </script>
   ```

---

## 3. Membuat Komponen Lanjutan: App3.vue

Setelah memahami dasar, saya mencoba fitur Vue yang lebih kompleks, seperti:

- **Reactive Variables** dengan `ref`.
- **Lifecycle Hooks** dengan `onMounted`.
- **Manipulasi Array** untuk menambah dan menghapus data.

### Apa yang Saya Pelajari:

1. **ref**: Untuk membuat variabel reaktif.
2. **onMounted**: Lifecycle hook untuk mengambil data dari API ketika komponen dimuat.
3. **Event Binding**: Form submission dan penghapusan data menggunakan event.

### Kode:

Berikut adalah kode yang saya buat di file `App3.vue`:

```vue
<script setup>
import { ref, onMounted } from "vue";

const name = ref("Sapri");
const status = ref("active");
const tasks = ref(["Tugas 1", "Tugas 2", "Tugas 3"]);
const newTask = ref("");

const toggleStatus = () => {
	status.value = status.value === "active" ? "pending" : "active";
};

const addTask = () => {
	if (newTask.value !== "") {
		tasks.value.push(newTask.value);
		newTask.value = "";
	}
};

const deleteTask = (index) => {
	tasks.value.splice(index, 1);
};

onMounted(async () => {
	try {
		const response = await fetch("https://jsonplaceholder.typicode.com/todos");
		const data = await response.json();
		tasks.value = data.map((task) => task.title);
	} catch (error) {
		console.error(error);
	}
});
</script>

<template>
	<h1>{{ name }}</h1>
	<h1 v-if="status == 'active'">User is Active</h1>
	<h1 v-else-if="status == 'pending'">User is Pending</h1>
	<h1 v-else>User is Not Active</h1>

	<form @submit.prevent="addTask">
		<label for="newTask">Tambahkan Tugas</label>
		<input
			type="text"
			id="newTask"
			v-model="newTask"
			placeholder="Tambahkan Tugas" />
		<button type="submit">Tambah</button>
	</form>

	<h3>Daftar Tugas:</h3>
	<ul>
		<li
			v-for="(task, index) in tasks"
			:key="task">
			<span>{{ task }}</span>
			<button @click="deleteTask(index)">Hapus</button>
		</li>
	</ul>

	<button @click="toggleStatus">Ubah Status</button>
</template>
```

### Cara Saya Gunakan:

1. Saya simpan kode di file `App3.vue` di folder `src/components`.
2. Lalu, saya impor komponen ini ke dalam `App.vue`:

   ```vue
   <template>
   	<App3 />
   </template>

   <script>
   import App3 from "./components/App3.vue";

   export default {
   	components: {
   		App3,
   	},
   };
   </script>
   ```

---

## 4. Menjalankan Proyek

Untuk menjalankan aplikasi, saya cukup menggunakan perintah berikut:

```bash
pnpm dev
```

Lalu, saya akses proyek di browser melalui `http://localhost:5173`.

---

## Catatan Tambahan

- Saya mulai belajar **Vue directives** seperti `v-bind`, `v-model`, dll.
- Ke depan, saya ingin mengeksplorasi **Vue Router** untuk navigasi dan **Pinia** untuk manajemen state.
