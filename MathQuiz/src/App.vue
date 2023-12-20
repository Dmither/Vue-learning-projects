<script setup>
import { ref } from 'vue';
import OperatorSelector from "./components/OperatorSelector.vue"
import OperatorQuiz from "./components/OperatorQuiz.vue"

const operator = ref(null);

function selectOperator(op) {
  operator.value = op;
}
function clearOperator() {
  operator.value = null;
}
</script>

<template>
  <div id="app">
    <h1>Math Quiz App</h1>
    <OperatorSelector v-if="!operator" @changeOperator="selectOperator"/>
    <!-- <OperatorSelector @changeOperator="selectOperator"/> -->
    <OperatorQuiz v-if="operator" :operator="operator" @onBack="clearOperator"/>
  </div>
</template>

<style scoped>
#app {
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  color: #022e39;
}

h1 {
  text-align: center;
}
</style>

<!-- https://www.youtube.com/watch?v=y7dh6NrwlPI -->
<!-- 17:35 -->