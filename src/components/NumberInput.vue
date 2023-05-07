<script setup lang="ts">
import { PropType } from "vue"

interface ModelModifiers {
    numberOnly?: boolean
}

const emits = defineEmits<{
    (e: 'update:modelValue', newValue: number): void
}>()

const props = defineProps({
    modelValue: {
        type: Number,
        default: 0
    },
    modelModifiers: {
        type: Object as PropType<ModelModifiers>,
        default: () => ({})
    }
});

function emitValue(event: Event) {
    const inputEvent = event as InputEvent
    const value = (inputEvent.target as HTMLInputElement).value
    let newValue: number = Number(value)
    if (props.modelModifiers.numberOnly && value === '') {
        newValue = 0
    }
    emits('update:modelValue', newValue)
}
</script>

<template>
    <input type="number" :value="modelValue" @input="emitValue" />
</template>