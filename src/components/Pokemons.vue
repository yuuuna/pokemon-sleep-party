<script setup>
import { ref } from 'vue'
import pokemons from '@/json/pokemons.json';
import fruits from '@/json/fruits.json';
import ingredients from '@/json/ingredients.json';

let filterData = ref({
    "fruits": [],
    "ingredients": []
})
let pokemonList = ref([]);
filterPokemon();


function filterFruit(fruitId) {
    let fruitList = filterData.value.fruits;
    if (fruitList.includes(fruitId)) {
        // 有找到，移除
        let index = fruitList.findIndex((id) => id === fruitId);
        fruitList.splice(index, 1);
    } else {
        // 沒找到，新增
        fruitList.push(fruitId);
    }
    filterPokemon();
}

function filterIngredient(ingredientId) {
    let ingredientList = filterData.value.ingredients;
    if (ingredientList.includes(ingredientId)) {
        // 有找到，移除
        let index = ingredientList.findIndex((id) => id === ingredientId);
        ingredientList.splice(index, 1);
    } else {
        // 沒找到，新增
        ingredientList.push(ingredientId);
    }
    filterPokemon();
}

function filterPokemon() {
    if (filterData.value.fruits.length === 0 && filterData.value.ingredients.length === 0) {
        pokemonList.value = pokemons;
        return;
    }
    let pokemonTempData = pokemons;

    if (filterData.value.fruits.length > 0) {
        pokemonTempData = pokemonTempData.filter((pokemon) => filterData.value.fruits.includes(pokemon.fruit_id));
    }

    if (filterData.value.ingredients.length > 0) {
        console.log('in');
        pokemonTempData = pokemonTempData.filter((pokemon) => pokemon.ingredients_id.some((ingre) => filterData.value.ingredients.includes(ingre)));
    }
    
    pokemonList.value = pokemonTempData;
}

</script>

<template>
    <p class="d-inline-flex gap-1">
        <a class="btn btn-primary" data-bs-toggle="collapse" href="#collapseFilter" role="button" aria-expanded="false"
            aria-controls="collapseFilter">
            Filter
        </a>
    </p>
    <div class="collapse" id="collapseFilter">
        <div class="card card-body">
            <h3>過濾條件</h3>
            <div class="row">
                <div class="col-2">樹果</div>
                <div class="col-10 fruit-filter">
                    <div v-for="fruit in fruits" class="fruit-card"
                        :class="{ clicked: filterData.fruits.includes(fruit.id) }" @click="filterFruit(fruit.id)">
                        <span class="fruit-title">{{ fruit.name }}</span>
                        <img class="fruit-img pt-1 pb-1" :src="`./images/fruits/${fruit.id}.png`" />
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-2">食材</div>
                <div class="col-10 fruit-filter">
                    <div v-for="ingredient in ingredients" class="fruit-card"
                        :class="{ clicked: filterData.ingredients.includes(ingredient.id) }"
                        @click="filterIngredient(ingredient.id)">
                        <span class="fruit-title">{{ ingredient.name }}</span>
                        <img class="fruit-img pt-1 pb-1" :src="`./images/ingredients/${ingredient.id}.png`" />
                    </div>
                </div>
            </div>
        </div>
    </div>
    <table class="table table-striped">
        <thead>
            <tr>
                <td>編號</td>
                <td>名字</td>
                <td>樹果</td>
                <td>食材</td>
                <td>地點</td>
                <td>主技能</td>
                <td>專長</td>
                <td>睡覺類型</td>
            </tr>
        </thead>
        <tbody>
            <tr v-for="pokemon in pokemonList">
                <td>{{ pokemon.id }}</td>
                <td>{{ pokemon.name }}</td>
                <td>
                    <img class="fruit-img" :src="`./images/fruits/${pokemon.fruit_id}.png`" />
                    {{ pokemon.fruit }}
                </td>
                <td>
                    <span v-for="(ingredient, index) in pokemon.ingredients">
                        {{ (index > 0 ? "、" : "") }} <img class="fruit-img"
                            :src="`./images/ingredients/${ingredient.id}.png`" /> {{ ingredient.name }}
                    </span>
                </td>
                <td>{{ pokemon.place }}</td>
                <td>{{ pokemon.skill }}</td>
                <td><span class="badge text-bg-primary">{{ pokemon.expertise }}</span></td>
                <td>{{ pokemon.sleep_type }}</td>
            </tr>
        </tbody>
    </table>
</template>

<style scoped>
.fruit-filter {
    display: flex;
    justify-content: space-around;
    align-items: center;
}

.fruit-card {
    display: flex;
    flex-direction: column;
    align-items: center;

    &.clicked {
        background-color: #b0ddff;
        border: #8bb5d4 solid 1px;
        border-radius: 5px;
    }
}

.fruit-title {
    font-size: 0.75rem;
}

.fruit-img {
    width: 20px;
}

.btn-filter {
    width: 100px;
}
</style>
