<template>
  <TheHeader text='My Counter' />
  <div v-if="!validationMessageList.length">{{ count }}</div>
  <div v-else v-for="message in validationMessageList" :key="message">
    {{ message }}
  </div>
  <BaseButton :disabled="hasMaxCount" @click="plusOne">+</BaseButton>
  <BaseButton :disabled="hasMinCount" @click="minusOne">-</BaseButton>

  <NumberInput v-model.numberOnly="inputCount" max="9999" min="0" />

  <BaseButton @onClick="insertCount">insert</BaseButton>

  <br />
  <button @click="toggleIsShow">isShow</button>
  <div v-if="isShow">{{ text }}</div>
</template>

<script setup lang="ts">
import TheHeader from './components/TheHeader.vue'
import BaseButton from "./components/BaseButton.vue";
import NumberInput from "./components/NumberInput.vue"
import { ref, computed, watch, onBeforeMount, onUpdated, onBeforeUnmount, onUnmounted, onBeforeUpdate, onMounted, provide } from 'vue';

const count = ref(0);
const inputCount = ref(0);
const isEditing = ref(false);

const hasMaxCount = computed(() => count.value >= 9999);
const hasMinCount = computed(() => count.value <= 0);
const hasMaxInputCount = computed(() => inputCount.value > 9999);
const hasMinInputCount = computed(() => inputCount.value < 0);

const validationMessageList = computed(() => {
  const validationList = []
  if (isEditing.value) {
    validationList.push("編集中///")
  }
  if (hasMaxInputCount.value) {
    validationList.push("9999///")
  }
  if (hasMinInputCount.value) {
    validationList.push("0///")
  }
  return validationList
});

watch(inputCount, () => {
  isEditing.value = true;
});

function plusOne() {
  count.value++;
}

function minusOne() {
  count.value--;
}

function insertCount() {
  if (hasMaxInputCount.value || hasMinInputCount.value) return
  count.value = inputCount.value;
  isEditing.value = false;
}

// life-cycle hook
const isShow = ref(true);
const text = ref("")

function toggleIsShow() {
  isShow.value = !isShow.value
}

onBeforeMount(() => {
  console.log("on before mount")
})

onMounted(() => {
  console.log("on mount")
})

onBeforeUpdate(() => {
  console.log("on before update", text.value)
})

onUpdated(() => {
  console.log("on update", text.value)
})

onBeforeUnmount(() => {
  console.log("on before unmounted")
})

onUnmounted(() => {
  console.log("on unmounted")
})

console.log("on created")


// inject-provide
provide("unique", "My Counter 2")


</script>

<style scoped></style>
