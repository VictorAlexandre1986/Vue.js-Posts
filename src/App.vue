<script setup>
import {ref, onMounted} from 'vue'

//Components
import BlogPost from './components/BlogPost.vue'
import PaginacaoPagina from './components/PaginacaoPagina.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

// const posts = ref([
//   {title: "First Post", content:"This is the first post.", id:"1"},
//   {title: "Second Post", content:"This is the second post.", id:"2"},
//   {title: "Third Post", id:"3"},
// ]);

const posts = ref([]);
const favorito = ref('');
const postPagina = 5;
const inicio = ref(0);
const fim = ref(postPagina);
const loading = ref(true);


const trocarFavorito = (escolhido) =>{
    favorito.value = escolhido;
}

const avancarPosts = () =>{
  inicio.value = inicio.value +  postPagina;
  fim.value = fim.value + postPagina;
}

const retrocederPosts = () =>{
    inicio.value =  inicio.value - postPagina;
    fim.value =  fim.value - postPagina;
}


onMounted(async () =>{
  loading.value= true;
  try{
    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    posts.value = await res.json()
  }
  catch(e){
    console.log(e);
  }
  finally{
    loading.value = false;
  }
})


</script>


<template>
  
  <header>
  </header>

  <main>
    <LoadingSpinner v-if="loading"/>
    
    <div v-else >
        <h1 class="text-center mb-5">POSTS</h1>

        <h2>Meu post favorito : {{ favorito}}</h2>

    

        <BlogPost
              v-for="post in posts.slice(inicio,fim)" 
              :key="post.id"
              :id="post.id"
              :title="post.title" 
              :body="post.body" 
              @trocarFavorito="trocarFavorito"
              />


              <PaginacaoPagina           
              @retrocederPosts="retrocederPosts"
              @avancarPosts="avancarPosts"
              :inicio="inicio"
              :fim="fim"
              :maxLength="posts.length"/>
              
      </div>
  </main>
</template>

<style scoped>
</style>
