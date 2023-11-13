<script setup>
import { ref, reactive } from "vue"
const current = ref("");
const last = ref("");
const operator = ref("");

function clear() {
  last.value = "";
  operator.value = "";
  current.value = "0";
}
function sign() {
  if (current.value) {
    current.value = current.value.charAt(0) === "-" ? current.value.slice(1) : `-${current.value}`
  }
}
function percent() {
  if (current.value) {
    current.value = `${parseFloat(current.value) / 100}`
  }
}
function dot() {
  if (current.value.indexOf(".") === -1) {
    current.value = `${current.value}.`
  }
}
function append(number) {
  if (current.value.length < 18) {
    if (Number(current.value) == 0 && current.value.indexOf(".") == -1) {
      current.value = current.value.charAt(0) === "-" ? "-" : ""
    }
    current.value = `${current.value}${number}`
  }
}
function operation(op) {
  if (op === "-" && Number(current.value) === 0) {
    sign();
    return;
  }
  if (last.value) {
    sum()
  }
  operator.value = op;
  last.value = current.value;
  current.value = "0";
}
function sum() {
  if (operator.value === "/") {
    if (Number(current.value) == 0) return;
    current.value = `${Number(last.value) / Number(current.value)}`;
  }
  if (operator.value === "x") {
    current.value = `${Number(last.value) * Number(current.value)}`;
  }
  if (operator.value === "-") {
    current.value = `${Number(last.value) - Number(current.value)}`;
  }
  if (operator.value === "+") {
    current.value = `${Number(last.value) + Number(current.value)}`;
  }
  last.value = "";
  operator.value = "";
}

</script>

<template>
  <div class="calculator">
    <div class="display">
      <div class="display-last">{{ last || ""}} {{ operator }}</div>
      <div class="display-main">{{ current || "0"}}</div>
    </div>
    <button @click="clear" class="btn">C</button>
    <button @click="sign" class="btn">+/-</button>
    <button @click="percent" class="btn">%</button>
    <button @click="() => operation('/')" class="btn operator">/</button>
    <button @click="() => append(7)" class="btn">7</button>
    <button @click="() => append(8)" class="btn">8</button>
    <button @click="() => append(9)" class="btn">9</button>
    <button @click="() => operation('x')" class="btn operator">x</button>
    <button @click="() => append(4)" class="btn">4</button>
    <button @click="() => append(5)" class="btn">5</button>
    <button @click="() => append(6)" class="btn">6</button>
    <button @click="() => operation('-')" class="btn operator">-</button>
    <button @click="() => append(1)" class="btn">1</button>
    <button @click="() => append(2)" class="btn">2</button>
    <button @click="() => append(3)" class="btn">3</button>
    <button @click="() => operation('+')" class="btn operator">+</button>
    <button @click="() => append(0)" class="btn btn-double">0</button>
    <button @click="dot" class="btn">.</button>
    <button @click="sum" class="btn operator">=</button>

  </div>
</template>

<style scoped>
.calculator {
  background-color: #555;
  padding: 1px;
  max-width: 300px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  gap: 1px;
}

.display {
  padding: 10px 20px;
  grid-column: 1 / 5;
  background-color: #2f2f2f;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: center;
  color: #fff;
}

.display-last {
  height: 1rem;
  line-height: 1rem;
}
.display-main {
  font-size: 2rem;
}

.btn {
  border: none;
  background-color: #eee;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 1.2rem;
  transition: all 0.1s ease 0s;
}

.btn:hover,
.btn:focus-visible {
  background-color: #ddd;
}

.btn-double {
  grid-column: span 2;
}

.operator {
  background-color: rgb(210, 137, 3);
  color: #fff;
}

.operator:hover,
.operator:focus-visible {
  background-color: rgb(182, 119, 2);
}
</style>