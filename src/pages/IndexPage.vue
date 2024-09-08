<template>
  <q-page class="q-pa-md flex flex-center">
    <div class="calculator">
      <q-input
        v-model="display"
        class="calculator-display"
        readonly
        outlined
        dense
      />
      <div class="calculator-buttons">
        <q-btn v-for="button in buttons" :key="button.label" @click="onButtonClick(button)" :label="button.label" color="primary" flat />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue';

const display = ref('0');

const buttons = [
  { label: 'C' }, { label: '/' }, { label: '*' }, { label: 'DEL' },
  { label: '7' }, { label: '8' }, { label: '9' }, { label: '-' },
  { label: '4' }, { label: '5' }, { label: '6' }, { label: '+' },
  { label: '1' }, { label: '2' }, { label: '3' }, { label: '=' },
  { label: '0' }, { label: '.' }
];

const onButtonClick = (button) => {
  if (button.label === 'C') {
    display.value = '0';
  } else if (button.label === 'DEL') {
    display.value = display.value.slice(0, -1) || '0';
  } else if (button.label === '=') {
    try {
      display.value = eval(display.value).toString();
    } catch {
      display.value = 'Error';
    }
  } else {
    if (display.value === '0') {
      display.value = button.label;
    } else {
      display.value += button.label;
    }
  }
};
</script>

<style scoped>
.calculator {
  max-width: 400px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.calculator-display {
  width: 100%;
  text-align: right;
  font-size: 2em;
  margin-bottom: 10px;
}

.calculator-buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.q-btn {
  height: 60px;
  font-size: 1.5em;
}
</style>