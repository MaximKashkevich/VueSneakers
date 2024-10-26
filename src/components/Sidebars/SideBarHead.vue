<template>
    <div>
        <img @click="toggleSideBar" class="ml-5 cursor-pointer rotate-180" width="30" height="30"
            src="/SideBarImg/exit-svgrepo-com.svg" alt="Exit">
        <h1 class="font-bold text-[24px] leading-[29.05px] mt-4 ml-5 mb-6">Корзина</h1>
    </div>
</template>

<script setup>
import { inject } from 'vue';

const { toggleSideBar } = inject('sidebar'); // Получаем метод
</script>