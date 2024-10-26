<template>
    <main class="fixed w-full h-full bg-black opacity-60 z-20"></main>
    <section class="fixed z-30 w-[90%] md:w-[30%] bg-white h-full right-0 flex flex-col overflow-y-auto">
        <nav class="p-4">
            <SideBarHead :toggleSideBar="toggleSideBar" />
            <!-- Карточки -->
            <div>
                <SideBarCardList :sneakers="sneakers" :cart="cart" />
            </div>

            <nav>
                <div class="flex gap-2 mx-5 mt-3">
                    <span>Итого:</span>
                    <div class="flex-1 border-b border-dashed"></div>
                    <b>{{ totalPrice }} руб.</b>
                </div>
                <div class="flex gap-2 mx-5 mt-3">
                    <span>Налог 5%:</span>
                    <div class="flex-1 border-b border-dashed"></div>
                    <b>{{ discountedPrice }} руб.</b>
                </div>
                <button
                    class="py-5 w-full rounded-[18px] items-center flex justify-center bg-lime-500 mt-3 transition hover:-translate-y-1">
                    <span class="flex items-center">
                        <b class="text-white mr-3">Оформить заказ</b>
                        <img src="/public/SideBarImg/enter.svg" alt="enter">
                    </span>
                </button>
            </nav>
        </nav>
    </section>
</template>

<script setup>

import SideBarCardList from './SideBarCardList.vue';
import SideBarHead from './SideBarHead.vue';
import { computed, defineProps } from 'vue';

const props = defineProps({
    totalPrice: Number,
    toggleSideBar: Function
})

// Вычисляем налог (5% от totalPrice)
const discountedPrice = computed(() => props.totalPrice * 0.05);

</script>