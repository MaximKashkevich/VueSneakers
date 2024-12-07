<template>
  <SideBar :toggleSideBar="toggleSideBar" :totalPrice="totalPrice" v-if="sideBarOpen" />
  <main class=" w-4/5 h-full bg-white m-auto rounded-[20px] pb-10">
    <Header :toggleSideBar="toggleSideBar" :totalPrice="totalPrice" />
    <div class="border-b mt-10"></div>
    <section class="mt-10">
      <!-- ПОИСК -->
      <nav class="items-center">
        <img class="m-auto" src="/public/assets/generalLogo.png" alt="generalLogo">
      </nav>
      <nav class="flex flex-col md:flex-row justify-between items-center mx-5 md:mx-10 my-5">
        <div class="text-center md:text-left">
          <h1 class="font-bold text-[32px]">Все кроссовки</h1>
        </div>
        <div class="w-full md:w-auto my-3 md:my-0">
          <select @change="onChangeSort"
            class="w-full md:w-auto bg-white border border-gray-300 text-gray-700 py-2 px-3 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-300 transition">
            <option value="title">По названию</option>
            <option value="-price">По цене(дорогие)</option>
            <option value="price">По цене(дешевые)</option>
          </select>
        </div>
        <div class="relative w-full md:w-auto my-3 md:my-0">
          <img class="absolute top-[15px] left-[10px]" src="/public/assets/search.svg" alt="search">
          <input v-model="searchQuery" @input="onChangeSearch"
            class="px-8 py-3 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-300 transition bg-white text-gray-700 placeholder-gray-500 focus:bg-white"
            placeholder="Поиск" type="text" />
        </div>
      </nav>
      <!-- КАРТОЧКИ -->

      <CartSneakerList :onClickAddPlus="onClickAddPlus" :addToFavorites="addToFavorites" :sneakers="sneakers" />
    </section>
  </main>


</template>

<script setup>
import axios from 'axios'

import Header from "/src/components/Header.vue"
import CartSneakerList from './components/CartSneakerList.vue'
import SideBar from "./components/Sidebars/SideBar.vue";

import { onMounted, provide, ref, watch, computed } from "vue";

//Кроссовки
const sneakers = ref([]);

// Корзина
const cart = ref([])

//Общая стоимость
const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))

//Поиск
const searchQuery = ref('')

//Сортировка
const sortBy = ref('')

//Открытый ли боковой меню
const sideBarOpen = ref(false)
const toggleSideBar = () => {
  sideBarOpen.value = !sideBarOpen.value;
};

//Обновление значния поиска и сортировки
const onChangeSearch = event => {
  searchQuery.value = event.target.value;
}

const onChangeSort = event => {
  sortBy.value = event.target.value;
}

//Запрос на получение кроссовок

const fetchSneakers = async () => {
  try {
    const { data } = await axios.get(
      `https://0e24b4ab02c94085.mokky.dev/sneakers?title=*${searchQuery.value}&sortBy=${sortBy.value}`
    );
    sneakers.value = data.map((obj) => {
      return {
        ...obj,
        isAdded: false,
        isFavorites: false,
      }
    });
  } catch (e) {
    console.error(e);
  }
};

//Запрос на получение избранных:

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://0e24b4ab02c94085.mokky.dev/favorites')
    sneakers.value = sneakers.value.map((item) => {//Пробегаемся по массиву(+переобновляем) кроссовок и делаем проверку
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)//для каждой кроссовки, был ли добавляен кроссовок в favorites
      if (favorite) {
        return {
          ...item,
          isFavorites: true, //если был добавлен в избранное, добавляем isFavorites: true,
          favoriteId: favorite.id //Делаем сохранение айди избранных
        }
      } else {
        return item
      }
    })
  } catch (e) {
    console.log(e)
  }
  //На этапе запроса избранных товаров, пробегаемся о основному массиву sneakers и делаем поиск
  //
}

//Добавление избранных:
const addToFavorites = async (sneaker) => {
  try {
    if (!sneaker.isFavorites) {
      const obj = {
        parentId: sneaker.id
      }
      const { data } = await axios.post(`https://0e24b4ab02c94085.mokky.dev/favorites`, obj)
      sneaker.isFavorites = true
      sneaker.favoriteId = data.id //Сохраняем айди добавленных в избранное
    } else {
      await axios.delete(`https://0e24b4ab02c94085.mokky.dev/favorites/${sneaker.favoriteId}`)
      sneaker.isFavorites = false
      sneaker.favoriteId = null //Удаляем айди добавленных в избранное, если удаляется из избранного
    }
  } catch (e) {
    console.log(e)
  }
}

//Добавление в корзину:

const onClickAddPlus = (sneaker) => {
  if (!sneaker.isAdded) {
    addToCart(sneaker)
  } else {
    removeFromCart(sneaker)
  }
}

// Удаление карточки:

const removeFromCart = (sneaker) => {
  cart.value.splice(cart.value.indexOf(sneaker), 1)
  sneaker.isAdded = false
}

//Добавление карточки:

const addToCart = (sneaker) => {
  cart.value.push(sneaker)
  sneaker.isAdded = true
}

onMounted(async () => {
  await fetchSneakers();
  await fetchFavorites()
});

watch([searchQuery, sortBy], () => {
  fetchSneakers();
})

provide('cart', {
  cart,
  removeFromCart,
  addToCart,
}
)

provide('sidebar', {
  sideBarOpen,
  toggleSideBar,
});

</script>
