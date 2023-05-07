<template>
  <TheHeader text='My Counter' />
  <div v-if="!validationMessageList.values.length">{{ count }}</div>
  <div v-else v-for="message in validationMessageList.values" :key="message">
    {{ message }}
  </div>
  <BaseButton :disabled="hasMaxCount" @click="plusOne">+</BaseButton>
  <BaseButton :disabled="hasMinCount" @click="minusOne">-</BaseButton>

  <NumberInput v-model.numberOnly="inputCount" max="9999" min="0" />
  <BaseButton @onClick="insertCount">insert</BaseButton>
</template>


<script lang="ts">
import { ref, computed, watch, defineComponent, reactive } from "vue";
import TheHeader from './components/TheHeader.vue'
import BaseButton from "./components/BaseButton.vue";
import NumberInput from "./components/NumberInput.vue"

export default defineComponent({
  components: {
    TheHeader,
    BaseButton,
    NumberInput
  },
  setup() {
    const count = ref(0)
    const inputCount = ref(0)
    const isEditing = ref(false)

    const hasMaxCount = computed(() => {
      return count.value >= 9999
    })
    const hasMinCount = computed(() => {
      return count.value <= 0
    })
    const hasMaxInputCount = computed(() => {
      return inputCount.value > 9999
    })
    const hasMinInputCount = computed(() => {
      return inputCount.value < 0
    })
    const validationMessageList = computed(() => {
      const validationList = reactive<String[]>([])
      if (isEditing) {
        validationList.push("編集中///")
      }
      if (hasMaxInputCount) {
        validationList.push("9999///")
      }
      if (hasMinInputCount) {
        validationList.push("0///")
      }
      return validationList
    })

    function plusOne() {
      count.value++;
    }
    function minusOne() {
      count.value--;
    }
    function insertCount() {
      if (hasMaxInputCount.value || hasMinInputCount.value) return
      count.value = inputCount.value;
      isEditing.value = false
    }
    watch(inputCount, () => {
      isEditing.value = true
    })
    return {
      count,
      inputCount,
      isEditing,
      hasMaxCount,
      hasMinCount,
      validationMessageList,
      plusOne,
      minusOne,
      insertCount,
    }
  }
})

</script>

<style scoped></style>
