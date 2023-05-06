<template>
    <input type="number" :value="modelValue" @input="emitValue" />
</template>
<script lang="ts">
import { defineComponent, PropType } from "vue"

interface ModelModifiers {
    numberOnly?: boolean
}

export default defineComponent({
    emits: ['update:modelValue'],
    props: {
        modelValue: {
            type: Number,
            default: 0
        },
        modelModifiers: {
            type: Object as PropType<ModelModifiers>,
            default: () => ({})
        }
    },
    methods: {
        emitValue(event: Event) {
            const inputEvent = event as InputEvent
            const value = (inputEvent.target as HTMLInputElement).value
            let newValue: number = Number(value)
            if (this.modelModifiers.numberOnly && value === '') {
                newValue = 0
            }
            this.$emit('update:modelValue', newValue)
        }
    },
})
</script>