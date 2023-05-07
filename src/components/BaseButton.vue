<template>
    <button @click="handleClick">
        <slot />
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    setup(_, ctx) {
        function handleClick() {
            ctx.emit('onClick')
        }
        return {
            handleClick,
        }
    },
})


</script>

