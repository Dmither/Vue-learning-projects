<script setup>

</script>

<template>
  <div class="buttons">
    <button @click="$emit('changeOperator', '+')">Addition<br>(+)</button>
    <button @click="$emit('changeOperator', '-')">subtraction<br>(-)</button>
    <button @click="$emit('changeOperator', '/')">Division<br>(/)</button>
    <button @click="$emit('changeOperator', '*')">Multiplication<br>(*)</button>
  </div>
</template>

<style scoped>
.buttons {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

button {
  min-width: 150px;
  font-family: inherit;
  background-color: #d94b58;
  color: white;
  border: none;
  padding: 5px;
  font-size: 20px;
  cursor: pointer;
}
</style>