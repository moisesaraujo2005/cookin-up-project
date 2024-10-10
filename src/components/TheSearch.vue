<template>
       <div class="searchClass">Search
       <input class="searchBar" type="text" v-model="searchQuery" name="" id=""></div>
       <div class="alinhamentoSearch">
       <ul v-if="ingredientesFiltrados.length">
       <li v-for="(ingrediente, index) in ingredientesFiltrados" :key="index" @click="selecionarIngrediente(ingrediente)">
        {{ ingrediente }}
      </li></ul></div>
   
</template>

<script>

import { obterCategorias } from '@/http/index.js'; 

export default{

    data(){
        return {
            searchQuery: '',
            ingredienteList: []
        };

    },
    async created() {
        try{
      var categorias = await obterCategorias() 

      this.ingredienteList = categorias.flatMap(categoria => categoria.ingredientes || []);
     
  
    
    }
            
      catch(error) {
        console.log('deu erro viu moisés')
      }
    },
    computed:{
        ingredientesFiltrados() {
           return this.searchQuery ?
             this.ingredienteList.filter(ingrediente => 
          typeof ingrediente === 'string' &&  ingrediente.toLowerCase().includes(this.searchQuery.toLowerCase())) : []
        }
    },
    methods: {
    selecionarIngrediente(ingrediente) {
      this.$emit('ingredientSelected', ingrediente); 
      this.searchQuery = ''; 
    },
  },

}

</script>

<style scoped>
.searchClass{
    width: 10vw;
    display: flex;
    align-items: center;
    justify-content: center ;
    gap: 0.5rem;
}
.alinhamentoSearch{
    display: flex;
    justify-content: center;
    align-items: center;
}

.searchBar{
    width: 10vw;
    height: 5vh;
    border-radius: 10px;
}
ul {

}
li {
  padding: 10px;
  background-color: #f5f5f5;
  margin-bottom: 5px;
  cursor: pointer;
  width: auto;
}</style>