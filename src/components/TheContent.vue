<template>
  <main class="conteudo-principal">
    <section class="list">
     
      <span class="subtitulo-lg sua-lista-texto">
        Your list:
      </span>
      
    
      <ul v-if="ingredientes.length" class="ingredientes-sua-lista">
        <li v-for="(ingrediente, index) in ingredientes" :key="index" >
          <TagText :texto="ingrediente" ativa></TagText>
        </li>
      </ul>

   
      <p v-else class="paragrafo lista-vazia">
        <img src="../assets/icones/lista-vazia.svg" alt="">
        
Your list is empty, select ingredients to save.

      </p>
       <TheSearch @ingredientSelected="adicionarIngrediente" />
     
    </section>

   
    <TheSelectIngredient
      @adicionarIngrediente="adicionarIngrediente"
      @removerIngrediente="removerIngrediente"
    />

    
    <section v-if="ingredientes.length">
      <button @click="buscarReceitas">Search Recipes</button>
    </section>


    <section v-if="receitas.length">
      <span class="subtitulo-lg sua-lista-texto">
        Recipes found:
      </span>
      <ul class="receitas-lista">
        <li v-for="(receita, index) in receitas" :key="index">
          <a :href="receita.sourceUrl" target="_blank">
            <h3>{{ receita.title }}</h3>
            <img :src="receita.image" alt="Imagem da receita" />
          </a>
          <p><strong>Ingredients:</strong></p>
          <ul>
            <li v-for="(ingrediente, index) in receita.usedIngredients" :key="index">
              {{ ingrediente.name }}
            </li>
          </ul>
          <p v-if="receita.missedIngredients.length">
            <strong>Missing:</strong>
            <ul>
              <li v-for="(ingrediente, index) in receita.missedIngredients" :key="index">
                {{ ingrediente.name }}
              </li>
            </ul>
          </p>
        </li>
      </ul>
    </section>
  </main>
</template>
<script>
import TagText from './TagText.vue';
import TheSearch from './TheSearch.vue';
import TheSelectIngredient from './TheSelectIngredient.vue';

export default {
  data() {
    return {
      ingredientes: [], 
      receitas: [], 
     
      apiKey: '1319a0a6de0546aa942ab54126c394de', 
    };
  },
  components: {
    TheSelectIngredient,
    TagText,
    TheSearch
  },
  methods: {
 
    adicionarIngrediente(ingrediente) {
     
      if (!this.ingredientes.includes(ingrediente)) {
        this.ingredientes.push(ingrediente);
      
      }

     
    },


    removerIngrediente(ingrediente) {
      const index = this.ingredientes.indexOf(ingrediente);
      if (index !== -1) {
        this.ingredientes.splice(index, 1);
      }
    },

    async buscarReceitas() {
  console.log("Buscando receita");

  if (this.ingredientes.length === 0) {
    console.error("Nenhum ingrediente.");
    return;
  }

  const ingredientesString = this.ingredientes.join(','); 

  try {
    const response = await fetch(
      `https://api.spoonacular.com/recipes/findByIngredients?ingredients=${ingredientesString}&number=3&apiKey=${this.apiKey}&language=pt`
    );

    if (!response.ok) {
      throw new Error(` ${response.statusText}`);
    }

    const data = await response.json();
    console.log(`Receitas encontradas para os ingredientes:`, data);

    if (Array.isArray(data) && data.length > 0) {
      this.receitas = data;
    } else {
      console.log("Nenhuma receita encontrada .");
      this.receitas = [];
    }
  } catch (error) {
    console.error("Erro ao buscar", error);
  }
}

  },
};
</script>




<style scoped>

.receitas-lista {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 45vw;
}

.receitas-lista li {
  border: 1px solid #263A29;
  padding: 1rem;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  align-items: center;
}

.receitas-lista img {
  width:auto;
    height: 29vh;
   
   
    object-fit: cover;
    border-radius: 28px;
    border: 2px solid
}
.receitas-lista a{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}


button {
  background-color: #f0633c;
  color: white;
  padding: 1rem 2rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #e0512b;
}

.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

.sua-lista-texto {
  color: var(--coral, #F0633C);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}



.lista-vazia {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;

  color: var(--coral, #F0633C);
  text-align: center;
}

.list{
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  gap: 2vh;
}



@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>
