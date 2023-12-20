<script setup>
  defineProps(["operator"])
</script>

<template>
  <div>
    {{ operator }}
    <button @click="$emit('onBack')">ClearOperator</button>
  </div>
</template>

<style scoped>

</style>