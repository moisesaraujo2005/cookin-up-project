<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">
      Ingredients
    </h1>

    <p class="paragrafo-lg instrucoes">
      Select the ingredients you want to use in this recipe below:
    </p>

    <ul class="categorias">
      <li v-for="(categoria, index) in categorias" :key="index">
        <CardCategory :categoria="categoria"
        @adicionarIngrediente="$emit('adicionarIngrediente', $event)"
        @removerIngrediente="$emit('removerIngrediente', $event )"

        />
      </li>
    </ul>

    <p class="paragrafo dica">
      *Please note that you have salt, pepper and water at home.
    </p>

    
  </section>
</template>


<script>
import { obterCategorias } from '@/http/index.ts';
import CardCategory from './CardCategory.vue';





export default {
  data() {
    return {
      categorias: []
   
    }
    
  },
  async created() {
    this.categorias = await obterCategorias();
  },
  components:{
      CardCategory,
     
    },
    emits:['adicionarIngrediente', 'removerIngrediente']
}

</script>
<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>