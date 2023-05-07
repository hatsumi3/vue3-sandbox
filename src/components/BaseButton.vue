<script setup lang="ts">
const emit = defineEmits<{
    (e: 'onClick'): void
}>()

function handleClick() {
    emit('onClick');
}

</script>

<template>
    <button @click="handleClick">
        <slot />
    </button>
</template>


