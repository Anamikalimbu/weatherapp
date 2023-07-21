<template>
    <div class="w-screen h-screen bg-gradient-to-b from-black  to-green-500/50 from-50% ">
        <div class=" absolute bg-green-500/50 rounded-full -translate-x-1/2 -translate-y-1/2 pointer-events-none blur-3xl " :style="{ 
      left:`${x}px`,
      top:`${y}px`,
      width:`200px`, 
      height:`200px`}">

    </div>
        <header>
            <h1  class="text-center  text-xl text-white p-2 w-screen  bg-gradient-to-b from-black to-black">Weather Forecast</h1>
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
});

import { computed } from 'vue'
import { useMouse, useWindowSize } from '@vueuse/core'
const { x , y} = useMouse()
const { width, height } = useWindowSize()
const dx = computed (() =>Math.abs (x.value - width.value/2))
const dy = computed (() =>Math.abs (y.value - width.value/2))

</script>

<style lang="scss" scoped>

</style>