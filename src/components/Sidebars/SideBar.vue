<template>
    <main class="fixed w-full h-full bg-black opacity-50 z-20"></main>
    <section class="fixed z-30 w-[90%] md:w-[30%] bg-white h-full right-0">
        <nav class="p-4">
            <img @click="toggleSideBar" class="ml-8 cursor-pointer" width="20" height="20"
                src="/public/SideBarImg/Exit.svg" alt="Exit">
            <h1 class="font-bold text-[24px] leading-[29.05px] mt-4 mb-6">Корзина</h1>
            <SideBarCard />
        </nav>
    </section>
</template>

<script setup>
import SideBarCard from './SideBarCard.vue';
import { defineProps } from 'vue';

const props = defineProps({
    toggleSideBar: Function, //Получаем метод
    sideBarOpen: Boolean
})

const toggleSideBar = () => {
    props.toggleSideBar() //Вытаскиваем и вызываем метод
}
</script>