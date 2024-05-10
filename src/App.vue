<template>
  <div class="contacts">
    <!-- Formulir untuk menambahkan kontak baru -->
    <div class="add-contact">
      <input
        type="text"
        v-model="newContactName"
        placeholder="Nama Kontak"
      />
      <input
        type="tel"
        v-model="newContactNumber"
        placeholder="Nomor Telepon"
      />
      <button @click="addContact">Tambah Kontak</button>
    </div>
    
    <!-- Daftar kontak -->
    <ul>
      <li v-for="(contact, index) in contacts" :key="index">
        <div class="contact-info">
          <span class="contact-name">{{ contact.name }}</span>
          <span class="contact-phone">{{ contact.phone }}</span>
        </div>
        <button class="delete-btn" @click="deleteContact(index)">Hapus</button> <!-- Tombol hapus -->
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Referensi untuk daftar kontak dan input baru
const contacts = ref([]);
const newContactName = ref('');
const newContactNumber = ref('');

// Menambahkan kontak baru ke daftar
const addContact = () => {
  if (newContactName.value.trim() === '' || newContactNumber.value.trim() === '') {
    return; // Hindari penambahan kontak kosong
  }
  
  contacts.value.push({
    name: newContactName.value,
    phone: newContactNumber.value,
  });
  
  // Bersihkan input setelah menambahkan kontak
  newContactName.value = '';
  newContactNumber.value = '';
};

// Menghapus kontak dari daftar
const deleteContact = (index) => {
  contacts.value.splice(index, 1); // Menghapus kontak berdasarkan index
};
</script>

<style scoped>
.contacts {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  background: linear-gradient(to bottom, #e0eafc, #cfdef3); /* Gradasi warna baru */
  box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  margin: auto;
  font-family: 'Arial', sans-serif;
}

.add-contact {
  display: flex;
  gap: 10px;
  justify-content: center;
  margin-bottom: 20px;
}

.add-contact input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: all 0.3s;
}

.add-contact input:focus {
  border-color: #4CAF50;
  box-shadow: 0 0 10px rgba(76, 175, 80, 0.2);
}

.add-contact button {
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  cursor: pointer;
  transition: all 0.3s;
}

.add-contact button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  transition: all 0.3s;
}

.contact-info {
  display: flex;
  flex-direction: column;
}

.contact-name {
  font-weight: bold;
}

.contact-phone {
  color: #555;
}

li:hover {
  background-color: #f1f1f1;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
}

.delete-btn {
  padding: 5px 10px;
  border-radius: 5px;
  background-color: #f44336;
  color: white;
  transition: all 0.3s;
}

.delete-btn:hover {
  background-color: #e53935;
}
</style>
