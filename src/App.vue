<template>
  <div id="app">
    <CountryList />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CountryList from './components/CountryList.vue';

export default defineComponent({
  name: 'App',
  components: {
    CountryList,
  },
});
</script>
