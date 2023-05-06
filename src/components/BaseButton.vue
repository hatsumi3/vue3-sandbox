<template>
    <button @click="handleClick">
        <slot />
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    methods: {
        handleClick() {
            this.$emit('onClick')
        }
    }
})


</script>

