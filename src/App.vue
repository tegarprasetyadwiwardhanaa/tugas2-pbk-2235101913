<template>
  <div id="app" class="container">
    <h1>Sebut Nama Siswa</h1>
    <div class="input-section">
      <input
        v-model="namaSiswa"
        placeholder="Masukkan nama siswa"
        @input="cekNama"  
        :class="{ 'input-error': namaSiswa.trim() === '' }"
      />
      <button
        @click="sebutNama" 
        :disabled="namaSiswa.trim() === ''" 
        :class="buttonClass"
        :style="buttonStyle"
      >
        Sebut Nama
      </button>
    </div>
    <transition name="fade-in">
      <div v-if="pesan" class="result-box">
        {{ pesan }}
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      namaSiswa: "",  
      pesan: null, 
    };
  },
  methods: {
    sebutNama() {
      if (this.namaSiswa.trim() === "") {
        this.pesan = "Silakan masukkan nama siswa.";
      } else {
        this.pesan = `Nama siswa yang disebut: ${this.namaSiswa}`;
      }
    },
    cekNama() { 
      if (this.namaSiswa.trim() === "") {
        this.pesan = "Nama siswa tidak boleh kosong.";
      } else {
        this.pesan = null;
      }
    },
  },
  computed: {
    buttonClass() {
      return {
        'btn-primary': this.namaSiswa.trim() !== '',
        'btn-disabled': this.namaSiswa.trim() === '',
      };
    },
    buttonStyle() {
      return {
        backgroundColor: this.namaSiswa.trim() === '' ? 'gray' : '#3498db',
      };
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 200px;  /* Menggunakan seluruh tinggi tampilan */
  background-color: #f5f5f5;  /* Warna latar belakang yang lebih lembut */
  color: #2c3e50;
}

.input-section {
  display: flex;
  gap: 10px;  /* Menambahkan jarak antara input dan tombol */
  margin-bottom: 20px;
}

input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  transition: border-color 0.3s;
}

.input-error {
  border-color: red;  /* Warna border saat error */
}

button {
  padding: 10px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #2980b9;  /* Efek hover */
}

.btn-disabled {
  background-color: gray;
  color: #b0b0b0;
  cursor: not-allowed;
}

.result-box {
  padding: 15px;
  border: 2px solid #3498db;
  background-color: white;
  border-radius: 10px;  /* Sudut melengkung */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);  /* Bayangan */
  font-weight: bold;
  text-align: center;
}

.fade-in-enter-active, 
.fade-in-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.fade-in-enter, 
.fade-in-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
