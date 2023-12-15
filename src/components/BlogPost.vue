<script setup>

//É possível passar os props dos dois jeitos
// defineProps(['title', 'description','id'])

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Não foi passado nenhuma descricao'
    }
});



</script>

<template>
    <div class="card">
        <h3 class="card-title">{{ id }} - {{ title }}</h3>
        <p>{{ body }}</p>
        <button @click="$emit('trocarFavorito', title)">Favorito</button>

    </div>
</template>

<style scoped>

.card{
    margin-top: 1rem;
    padding: 2rem;
}

button{
    background-color: #181818;
    color:#fff;
    padding:0.5rem 1rem;
    border-radius: 0.7rem;
    font-size: 1rem;
    margin-bottom: 1rem;;
}
</style>