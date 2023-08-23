<script setup>
import pokemons from '@/json/pokemons.json';
</script>

<template>
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
            <tr v-for="pokemon in pokemons">
                <td>{{ pokemon.id }}</td>
                <td>{{ pokemon.name }}</td>
                <td>{{ pokemon.fruit }}</td>
                <td>{{ pokemon.ingredients }}</td>
                <td>{{ pokemon.place }}</td>
                <td>{{ pokemon.skill }}</td>
                <td>{{ pokemon.expertise }}</td>
                <td>{{ pokemon.sleep_type }}</td>
            </tr>
        </tbody>
    </table>
</template>
