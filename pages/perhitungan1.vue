<template>
  <div class="form-container">
    <h1>Form Investasi (Soal 1)</h1>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="jenis_kelamin">Jenis Kelamin:</label>
        <select v-model="form.jenis_kelamin" id="jenis_kelamin" required>
          <option value="pria">Pria</option>
          <option value="wanita">Wanita</option>
        </select>
      </div>

      <div class="form-group">
        <label for="usia">Usia:</label>
        <input type="number" v-model="form.usia" id="usia" required />
      </div>

      <div class="form-group">
        <label for="perokok">Perokok:</label>
        <select v-model="form.perokok" id="perokok" required>
          <option value="ya">Ya</option>
          <option value="tidak">Tidak</option>
        </select>
      </div>

      <div class="form-group">
        <label for="nominal">Nominal Investasi:</label>
        <input type="number" v-model="form.nominal" id="nominal" required/>
      </div>

      <div class="form-group">
        <label for="lama">Lama Investasi:</label>
        <input type="number" v-model="form.lama" id="lama" required min="1" />
      </div>

      <button type="submit">Submit</button>
    </form>

    <!-- Display API Response -->
    <div class="response-container" v-if="response">
      <h2>Investment Calculation Results</h2>
      <div v-for="(item, index) in response.data" :key="index">
        <p><strong>Year {{ index }}:</strong></p>
        <ul>
          <li>Awal: {{ item.awal }}</li>
          <li>Bunga: {{ item.bunga }}</li>
          <li>Akhir: {{ item.akhir }}</li>
        </ul>
      </div>
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
        perokok: '',  
        nominal: '',
        lama: '' 
      },
      response: null 
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await this.$axios.post('/api/perhitungan1', this.form);

        if (response.data && response.data.status === 200) {
          this.response = response.data;
        } else {
          alert('Unexpected response format.');
        }
      } catch (error) {
        console.error('Error submitting form:', error);
        alert('Failed to submit the form.');
      }
    }
  }
};
</script>