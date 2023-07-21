<template>
    <div>
        <header>
            <h1  class="text-center  text-xl p-2">Weather Forecast</h1>
            <Navbar />
        </header>

        <main>
            <slot>

            </slot>
        </main>
        <footer>
            <Last />
        </footer>
    </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { initFlowbite } from 'flowbite'

// initialize components based on data attribute selectors
onMounted(() => {
    initFlowbite();
})

</script>

<style lang="scss" scoped>

</style>