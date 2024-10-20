<template>
    <section class="mx-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-9">
        <CartSneakers v-for="item in sneakers" :key="item.id" :title="item.title" :imageUrl="item.imageUrl"
            :price="item.price" :isFavorites="item.isFavorites" :isAdded="item.isAdded"
            :addToFavorites="addToFavorites" />
    </section>
</template>


<script setup>
import { defineProps } from 'vue';
import CartSneakers from './CartSneakers.vue';

defineProps({
    sneakers: Array,
    addToFavorites: Function
})

</script>