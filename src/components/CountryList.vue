<template>
  <div class="container">
    <div class="country-list">
      <h1 id="header-title">Список стран</h1>
      <div v-if="loading">Загрузка...</div>
      <div class="grid-container" v-else>
        <div class="country-card" v-for="country in countries" :key="country.id">
          <div class="country-name">{{ country.name }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

interface Country {
  id: number;
  name: string;
}

export default defineComponent({
  name: 'CountryList',
  data() {
    return {
      countries: [] as Country[],
      loading: true,
    };
  },
  async created() {
    try {
      const response = await axios.get<Country[]>('http://all-countries.local/api/country');
      this.countries = response.data;
    } catch (error) {
      console.error('Ошибка при загрузке данных:', error);
    } finally {
      this.loading = false;
    }
  },
});
</script>

<style scoped>
@import '@/assets/fonts/fonts.css';

.container {
  background-color: #f5f5f5;
  height: 100vh;
  width: 100vw;
}

.country-list {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  text-align: left; 
  padding: 0;
}

#header-title {
  color: #42b983;
  font-weight: 700;
  font-size: 3.5em;
  font-family: 'Architectural-light';
  margin-top: 10px;
  margin-left: 10px;
  margin-bottom: 0px;
  padding: 0; 
  text-align: left; 
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  padding: 16px; /* Добавляем отступы для сетки */
  flex-grow: 1;
  overflow-y: auto;
  overflow-x: none;
  box-sizing: border-box;
  width: 100%;
}

.country-card {
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  aspect-ratio: 1 / 1;
  box-sizing: border-box;
}

.country-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.country-name {
  font-family: 'Architectural-light', sans-serif;
  font-weight: bold !important;
  font-size: 2.5em;
  color: #333;
  font-weight: 500;
  word-wrap: break-word;
  overflow: hidden;
}
</style>