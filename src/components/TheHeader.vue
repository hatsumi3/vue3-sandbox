<template>
    <header> {{ text }}</header>
</template>

<script setup lang="ts">
import { inject } from 'vue';

defineProps({
    text: {
        text: String,
        default: 'abc',
        required: true,
        validator: (value: String) => {
            // 空白orNullorUndefinedはfalse
            return !!value
        },
    }
});

const title = inject("unique")
console.log(title)


</script>

<style scoped>
header {
    font-size: 32px;
}
</style>

