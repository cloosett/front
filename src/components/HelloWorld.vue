<template>
  <div>
    <h1>hello world</h1>
    <div v-if="loading">Завантаження...</div>
    <div v-if="error">{{ error }}</div>
    <ul v-if="data.length">
      <li v-for="item in data" :key="item.id">{{ item.id }} - {{ item.title }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      data: [],
      loading: false,
      error: null
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      this.loading = true;
      this.error = null;

      try {
        const response = await axios.get('https://testingfantik.fun/api/books');
        console.log(response)
        this.data = response.data.data;
      } catch (err) {
        this.error = 'Не вдалося завантажити дані';
      } finally {
        this.loading = false;
      }
    }
  }
};
</script>

<style scoped>

</style>
