<template>
  <div class="form-container">
    <h1>Form Investasi (Soal 2)</h1>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="nama">Nama:</label>
        <input type="text" v-model="form.nama" id="nama" required />
      </div>

      <div class="form-group">
        <label for="jenis_kelamin">Jenis Kelamin:</label>
        <select v-model="form.jenis_kelamin" id="jenis_kelamin" required>
          <option value="pria">Pria</option>
          <option value="wanita">Wanita</option>
        </select>
      </div>

      <div class="form-group">
        <label for="perokok">Perokok:</label>
        <select v-model="form.perokok" id="perokok" required>
          <option value="ya">Ya</option>
          <option value="tidak">Tidak</option>
        </select>
      </div>

      <div class="form-group">
        <label for="usia">Usia :</label>
        <input type="number" v-model="form.usia" id="usia" required />
      </div>

      <div class="form-group">
        <label for="nominal">Nominal Investasi:</label>
        <input type="number" v-model="form.nominal" id="nominal" required />
      </div>

      <div class="form-group">
        <label for="lama">Lama Investasi:</label>
        <input type="number" v-model="form.lama" id="lama" required min="1" />
      </div>

      <div class="form-group">
        <label for="periode_pembayaran">Periode pembayaran:</label>
        <select v-model="form.periode_pembayaran" id="periode_pembayaran" required>
          <option value="bulanan">Bulanan</option>
          <option value="tahunan">Tahunan</option>
        </select>
      </div>

      <div class="form-group">
        <label for="metode_bayar">Metode bayar:</label>
        <select v-model="form.metode_bayar" id="metode_bayar" required>
          <option value="transfer">Transfer</option>
          <option value="kartu_kredit">Kartu Kredit</option>
        </select>
      </div>

      <button type="submit">Submit</button>
    </form>

    <!-- Display API Response -->
    <div class="response-container" v-if="response">
      <h2>Data Investasi</h2>
      <ul>
        <li><strong>No Transaksi:</strong> {{ response.no_transaction }}</li>
        <li><strong>Tanggal Transaksi:</strong> {{ response.tgl_transaksi }}</li>
        <li><strong>Nama:</strong> {{ response.nama }}</li>
        <li><strong>Jenis Kelamin:</strong> {{ response.jenis_kelamin }}</li>
        <li><strong>Perokok:</strong> {{ response.perokok }}</li>
        <li><strong>Usia:</strong> {{ response.usia }}</li>
        <li><strong>Nominal Investasi:</strong> {{ response.nominal }}</li>
        <li><strong>Lama Investasi:</strong> {{ response.lama }} tahun</li>
        <li><strong>Periode Pembayaran:</strong> {{ response.periode_pembayaran }}</li>
        <li><strong>Metode Bayar:</strong> {{ response.metode_bayar }}</li>
        <li><strong>Total Bayar:</strong> {{ response.total_bayar }}</li> <!-- Pastikan ini -->
      </ul>
    </div>
  </div>
</template>

<style scoped>
.form-container {
  max-width: 600px;
  margin: auto;
  padding: 1em;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
}

h1 {
  text-align: center;
  margin-bottom: 1rem;
}

.form-group {
  margin-bottom: 1rem;
  padding: 1em;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

.form-group input,
.form-group select {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  padding: 0.75rem 1.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}

button:hover {
  background-color: #0056b3;
}

.response-container {
  margin-top: 2rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #e9ecef;
}

.response-container h2 {
  margin-bottom: 1rem;
}

.response-container ul {
  padding-left: 1rem;
  margin-bottom: 1rem;
}
</style>

<script>
export default {
  data() {
    return {
      form: {
        nama: '',
        jenis_kelamin: '',
        usia: '',
        nominal: '',
        periode_pembayaran: '',
        metode_bayar: '',
        perokok: ''
      },
      response: null,
      no_transaction: null,
      tgl_transaksi:null
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await this.$axios.post('/api/perhitungan2', this.form);
        if (response.data && response.data.status === 200) {
          this.response = response.data.data;
          this.no_transaction = response.data.data.no_transaction;
          this.tgl_transaksi = response.data.data.tgl_transaksi;
        } else {
          alert('Gagal.');
        }
      } catch (error) {
        alert('Failed to submit the form.');
      }
    }
  }
}
</script>
