<script setup>
import fruits from '@/json/fruits.json';
</script>

<template>
    <h3>樹果清單</h3>
    <div class="row">
        <div v-for="fruit in fruits" class="fruit-card m-2 p-1 col-3 col-sm-2 col-lg-1" :class="`type-${fruit.type_en}`">
            <span class="fruit-title">{{ fruit.name }}</span>
            <img class="fruit-img pt-1 pb-1" :src="`./images/fruits/${fruit.id}.png`" />
            <div class="fruit-type">
                <img class="fruit-type-img" :src="`./images/types/${fruit.type_en}.png`" />&nbsp;{{ fruit.type }}
            </div>
        </div>
    </div>
</template>

<style scoped>
@import "@/assets/_pokemon.scss";

.fruit-card {
    background-color: var(--color);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 2px solid #AAA;
    border-radius: 10px;
}

.fruit-title {
    color: #FFF;
    font-weight: 900;
}

.fruit-img {
    width: 60%;
}

.fruit-type {
    color: #FFF;
    font-size: 0.75rem;
    font-weight: 600;
    display: flex;
    justify-content: center;
    align-items: center;
}

.fruit-type-img {
    width: 30%;
}
</style>
