<script setup>
import { onMounted, ref } from 'vue';
import { computed } from '@vue/reactivity';

const props = defineProps(["title", "timeOver", "date"])

const displayDays = ref("00");
const displayHours = ref("00");
const displayMinutes = ref("00");
const displaySeconds = ref("00");
const isOver = ref(false);
const isLoaded = ref(false);

const _seconds = computed(() => 1000);
const _minutes = computed(() => _seconds.value * 60);
const _hours = computed(() => _minutes.value * 60);
const _days = computed(() => _hours.value * 24)

function showRemaineng(endDate) {
  const distance = endDate.getTime() - new Date().getTime();
  if (distance < 0) {
    isOver.value = true;
    return
  }
  calculateData(distance);
  
  const timer = setInterval(() => {
    const distance = endDate.getTime() - new Date().getTime();
    if (distance < 1000) {
      isOver.value = true;
    }
    if (distance < 0) {
      clearInterval(timer);
      return
    }
    calculateData(distance)
  }, 1000)
}

function calculateData(distance) {
  const days = Math.floor(distance / _days.value)
  const hours = Math.floor((distance % _days.value) / _hours.value);
  const minutes = Math.floor((distance % _hours.value) / _minutes.value);
  const seconds = Math.floor((distance % _minutes.value) / _seconds.value);

  displayMinutes.value = minutes < 10 ? "0" + minutes : minutes;
  displaySeconds.value = seconds < 10 ? "0" + seconds : seconds;
  displayHours.value = hours < 10 ? "0" + hours : hours;
  displayDays.value = days < 10 ? "0" + days : days;
}

onMounted(() => {
  showRemaineng(props.date)
  isLoaded.value = true;
})

</script>

<template>
  <div class="wrapper" :class="{_over: isOver}" v-if="isLoaded">
    <div class="counter-title" v-if="!isOver">{{ props.title }}</div>
    <div class="counter-title" v-else>{{ props.timeOver }}</div>
    <div class="counter-table">
      <div class="counter-item counter-days">
        {{ displayDays }}
        <div class="counter-item-label">days</div>
      </div>
      <div class="counter-item-separator">:</div>
      <div class="counter-item counter-hours">
        {{ displayHours }}
        <div class="counter-item-label">hours</div>
      </div>
      <div class="counter-item-separator">:</div>
      <div class="counter-item counter-minutes">
        {{ displayMinutes }}
        <div class="counter-item-label">minutes</div>
      </div>
      <div class="counter-item-separator">:</div>
      <div class="counter-item counter-seconds">
        {{ displaySeconds }}
        <div class="counter-item-label">seconds</div>
      </div>
    </div>
  </div>
</template>

<style>
.wrapper {
  color: #243452;
}
.wrapper._over {
  color: rgb(161, 16, 16);
}
.counter-title {
  margin-bottom: 0.5rem;
  font-size: 1.5rem;
  text-align: center;
}

.counter-table {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  font-size: 3rem;
}

.counter-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 70px;
}

.counter-item-label {
  font-size: 1rem;
}
</style>