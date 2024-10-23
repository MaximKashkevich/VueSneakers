<script setup>
import { defineProps } from 'vue';
import CartSneakers from './CartSneakers.vue';

// const onClickFavorite = () => {
//     const obj = {
//         ...props,
//         parentId: props.id
//     }
//     props.addToFavorites(obj)
// } // будет только записывать определенную карточку

// :onClickFavorite="() => addToFavorites(item) - передача реактивного объекта

defineProps({
    sneakers: Array,
    addToFavorites: Function,
    onClickAddPlus: Function,
})


</script>

<template>
    <section class="mx-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-9">
        <CartSneakers v-for="item in sneakers" :key="item.id" :id="item.id" :title="item.title"
            :imageUrl="item.imageUrl" :price="item.price" :isFavorites="item.isFavorites" :isAdded="item.isAdded"
            :addToFavorites="addToFavorites" :onClickAddPlus="() => onClickAddPlus(item)"
            :onClickFavorite="() => addToFavorites(item)" />
    </section>
</template>