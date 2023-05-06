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
</template>


<script lang="ts">
import { defineComponent } from "vue";
import TheHeader from './components/TheHeader.vue'
import BaseButton from "./components/BaseButton.vue";
import NumberInput from "./components/NumberInput.vue"

export default defineComponent({
  components: {
    TheHeader,
    BaseButton,
    NumberInput
  },
  data() {
    return {
      count: 0,
      inputCount: 0,
      isEditing: false,
    }
  },
  computed: {
    hasMaxCount() {
      return this.count >= 9999
    },
    hasMinCount() {
      return this.count <= 0
    },
    hasMaxInputCount() {
      return this.inputCount > 9999
    },
    hasMinInputCount() {
      return this.inputCount < 0
    },
    validationMessageList() {
      const validationList = []
      if (this.isEditing) {
        validationList.push("編集中///")
      }
      if (this.hasMaxInputCount) {
        validationList.push("9999///")
      }
      if (this.hasMinInputCount) {
        validationList.push("0///")
      }

      return validationList
    }

  },
  watch: {
    inputCount() {
      this.isEditing = true
    }
  },
  methods: {
    plusOne() {
      this.count++;
    },
    minusOne() {
      this.count--;
    },
    insertCount() {
      if (this.hasMaxInputCount || this.hasMinInputCount) return
      this.count = this.inputCount;
      this.isEditing = false
    }
  }
})

</script>

<style scoped></style>
