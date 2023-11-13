<script setup>
import { ref } from 'vue';
import Counter from './Counter.vue';

const date = ref(new Date(2023, 10, 13, 12, 41));
</script>


<template>
  <h3>Hello, world!</h3>
  <Counter title="Left before the rocket launch:" timeOver="The rocket has launched" :date="date"></Counter>
</template>

<style scoped>

</style>