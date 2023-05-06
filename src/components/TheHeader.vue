<template>
    <header> {{ text }}</header>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    props: {
        text: {
            text: String,
            default: 'abc',
            required: true,
            validator: (value: String) => {
                // 空白orNullorUndefinedはfalse
                return !!value
            },
        }
    },
})

</script>

<style scoped>
header {
    font-size: 32px;
}
</style>

