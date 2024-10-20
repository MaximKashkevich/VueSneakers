<template>
    <header class="flex flex-col md:flex-row items-center justify-between mx-10 py-4shadow">
        <section class="flex items-center mt-4 md:mt-0">
            <img width="40" height="40" src="/public/HeaderImg/headerLogo.png" alt="headerLogo">
            <nav class="ml-4">
                <h1 class="font-bold leading-[24.2px] text-[20px]">REACT SNEAKERS</h1>
                <p class="text-gray-400">Магазин лучших кроссовок</p>
            </nav>
        </section>
        <section class="flex items-center mt-4 md:mt-0">
            <nav class="flex items-center mx-4">
                <img @click="toggleSideBar" class="cursor-pointer" src="/public/HeaderImg/shopHeader.svg"
                    alt="shopHeader">
                <p @click="toggleSideBar" class="leading-[16.94px] text-gray-600 mx-2 cursor-pointer">1205 руб.</p>
            </nav>
            <nav class="flex items-center mx-4">
                <img class="cursor-pointer" src="/public/HeaderImg/favoriteHeader.svg" alt="HeaderImg">
                <p class="leading-[16.94px] text-gray-600 mx-2 cursor-pointer">Закладки</p>
            </nav>
            <nav class="flex items-center mx-4">
                <img class="cursor-pointer" src="/public/HeaderImg/profileHeader.svg" alt="HeaderImg">
                <p class="leading-[16.94px] text-gray-600 mx-2 cursor-pointer">Профиль</p>
            </nav>
        </section>
    </header>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    sideBarOpen: Boolean,
    toggleSideBar: Function // Принимаем метод toggleSideBar 
});

const toggleSideBar = () => {
    props.toggleSideBar(); // Вызываем метод, полученный из props
};
</script>