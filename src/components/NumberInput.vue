<template>
    <input type="number" :value="modelValue" @input="emitValue" />
</template>

<script>

import { defineComponent } from "vue"
export default defineComponent({
    emits: ['update:modelValue'],
    props: {
        modelValue: {
            type: Number,
            default: 0
        },
        modelModifiers: {
            type: 
            default: () => ({})
        }
    },
    methods: {
        emitValue({ target: { value } }) {
            if (this.modelModifiers.numberOnly && value === '') {
                value = 0
            }
            this.$emit('update:modelValue', Number(value))
        }
    },
})
</script>