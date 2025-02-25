<template>
    <div class="country-list">
      <h1>Список стран</h1>
      <div v-if="loading">Загрузка...</div>
      <ul v-else>
        <li v-for="country in countries" :key="country.id">
          {{ country.name }}
        </li>
      </ul>
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
        loading: true, // Флаг загрузки
      };
    },
    async created() {
      try {
        const response = await axios.get<Country[]>('http://all-countries.wazowskii.ru/api/country');
        this.countries = response.data;
      } catch (error) {
        console.error('Ошибка при загрузке данных:', error);
      } finally {
        this.loading = false; // Загрузка завершена
      }
    },
  });
  </script>
  
  <style scoped>
  .country-list {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    text-align: center;
  }
  
  h1 {
    color: #42b983;
    margin-bottom: 20px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    padding: 10px;
    margin: 5px 0;
    border-radius: 4px;
    transition: background-color 0.3s ease;
  }
  
  li:hover {
    background-color: #e9e9e9;
  }
  </style>