<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  data() {
    return {
      message: 'Hello World'
    };
  }
});
</script>

<style scoped>
h1 {
  color: #42b983;
}
</style>