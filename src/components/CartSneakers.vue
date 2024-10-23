<template>
    <nav class="card">
        <img @click="onClickFavorite" class="favorite-icon"
            :src="isFavorites ? '/public/assets/favoriteTrue.svg' : '/public/assets/favoriteFalse.svg'" alt="favorite">
        <img class="sneaker-image" :src="props.imageUrl" alt="sneakerTest">
        <div class="description">
            <p>{{ title }}</p>
        </div>
        <div class="footer">
            <div class="price">
                <p class="price-label">ЦЕНА:</p>
                <span class="price-value">{{ price }} руб.</span>
            </div>
            <div class="add-icon">
                <img @click="onClickAddPlus"
                    :src="isAdded ? '/public/assets/addTrue.svg' : '/public/assets/addFalse.svg'" alt="add">
            </div>
        </div>
    </nav>
</template>
<script setup>
const props = defineProps({
    id: Number,
    price: Number,
    imageUrl: String,
    title: String,
    addToFavorites: Function,
    idAdd: Boolean,
    isFavorites: Boolean,
    onClickFavorite: Function,
    onClickAddPlus: Function
});
</script>

<style scoped>
.card {
    width: 100%;
    max-width: 300px;
    height: auto;
    background: white;
    border-radius: 30px;
    transition: all 0.3s ease;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    padding: 16px;
    position: relative;
}

.card:hover {
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
    transform: translateY(-5px);
}

.favorite-icon {
    position: absolute;
    top: 16px;
    left: 16px;
    cursor: pointer;
}

.sneaker-image {
    width: 100%;
    height: auto;
    max-width: 133px;
    max-height: 112px;
    margin: 16px auto;
}

.description {
    margin: 12px 0;
    text-align: center;
}

.footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.price {
    text-align: left;
}

.price-label {
    font-size: 14px;
    color: gray;
    font-weight: medium;
}

.price-value {
    font-weight: bold;
    display: block;
}

.add-icon img {
    width: 26px;
    /* подходящий размер для иконки */
    height: 26px;
    /* подходящий размер для иконки */
}

/* Адаптивность */
@media (max-width: 768px) {
    .card {
        padding: 12px;
    }

    .sneaker-image {
        max-width: 60%;
        /* уменьшаем изображение для меньших экранов */
    }
}

@media (max-width: 480px) {
    .favorite-icon {
        top: 8px;
        /* уменьшаем отступ на маленьких экранах */
        left: 8px;
        /* уменьшаем отступ на маленьких экранах */
    }

    .footer {
        flex-direction: column;
        /* меняем направление на маленьких экранах */
        align-items: flex-start;
    }

    .add-icon {
        margin-top: 8px;
    }
}
</style>