<script setup>
import personalities from '@/json/personality.json';
</script>

<template>
    <h3>個性清單</h3>
    <table class="table table-striped">
        <thead>
            <tr>
                <td>個性</td>
                <td>上升</td>
                <td>下降</td>
            </tr>
        </thead>
        <tbody>
            <tr v-for="personality in personalities">
                <td>{{ personality.name }}</td>
                <td class="personality-up"><i class="fa-regular fa-circle-up"></i>{{ personality.promote }}</td>
                <td class="personality-down"><i class="fa-regular fa-circle-down"></i>{{ personality.decline }}</td>
            </tr>
        </tbody>
    </table>
</template>

<style scoped>
.personality-up {
    color: #e16565;
}

.personality-down {
    color: #5b8ee1;
}
</style>
