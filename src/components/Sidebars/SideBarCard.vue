<template>
    <main class="flex justify-center mt-4">
        <section
            class="m-auto w-[90%] max-w-[325px] h-[auto] border rounded-[20px] flex items-center justify-between p-4">
            <nav>
                <img width="70px" height="70px" :src="imageUrl" alt="sneaketTest">
            </nav>
            <nav class="flex-1 px-2">
                <p class="leading-[16.94px] text-center">{{ title }}</p>
                <span class="font-bold leading-[16.94px] mt-2 block text-center">{{ price }} руб.</span>
            </nav>
            <nav>
                <img @click="onClickRemove" class="cursor-pointer" src="/public/SideBarImg/sneakerRemove.svg"
                    alt="sneakerRemove">
            </nav>
        </section>
    </main>
</template>

<script setup>
import { defineProps } from 'vue';

defineProps({
    id: Number,
    price: Number,
    imageUrl: String,
    title: String,
    onClickRemove: Function,
});

</script>
