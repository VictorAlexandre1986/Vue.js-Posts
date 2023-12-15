<script setup>
defineProps(['inicio','fim','maxLength']);

const emit = defineEmits(['AvancarPosts','RetrocederPosts']);
</script>

<template>
    <div class="botoes">
        <button  @click="emit ('RetrocederPosts')" :disabled="inicio <= 0">Anterior {{ inicio }}</button>
        <button @click="emit ('AvancarPosts')" :disabled="fim >= maxLength">Próximo {{ fim }}</button>
    </div>
</template>

<style scoped>
    .botoes{
        display: flex;
        justify-content: space-around;
        margin-top: 2rem;
    }

    button{
        background-color: #4CAF50; 
        color:#181818;
        padding:1rem 2rem;
        border-radius: 0.7rem;
        font-size: 1rem;
        margin: 0 1rem;
    }
</style>