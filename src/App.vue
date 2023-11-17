<template>
    <div class="center">
        <StandardBoard :hasWhite="hasWhite" :position="position"/>
    </div>
</template>

<style scoped>
    .center {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>

<script setup>
import StandardBoard from './components/Chessboard/StandardBoard.vue';
import data from './assets/startPosition.json'
    
    const hasWhite = (true)
    const position = new Map(Object.entries(data));

</script>