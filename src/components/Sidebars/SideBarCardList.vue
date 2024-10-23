<template>

    <SideBarCard v-for="item in cart" :key="item.id" :price="item.price" :imageUrl="item.imageUrl" :title="item.title"
        :onClickRemove="() => removeFromCart(item)" />

</template>

<script setup>
import SideBarCard from './SideBarCard.vue';
import { inject } from 'vue';

const { cart, removeFromCart, onClickAdd } = inject('cart')

</script>