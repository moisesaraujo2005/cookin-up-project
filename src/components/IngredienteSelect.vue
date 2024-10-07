<script>
import TagText from './TagText.vue';


export default{
    components:{
        TagText
    },
    props:{
        ingrediente:{type : String, required:true},
  
    },
    data() {
        return {
            selecionado:false
        }
    },
    methods:{
        aoClicar() {
            this.selecionado=!this.selecionado

            if(this.selecionado){
                this.$emit('adicionarIngrediente', this.ingrediente)
            }
            else {
                this.$emit('removerIngrediente', this.ingrediente)
            }
         

        },

      
        
   

    emits:['adicionarIngrediente', 'removerIngrediente']
}
}
</script>


<template>
        <button
        class="ingrediente"
        v-on:click="aoClicar()"
        :aria-pressed="selecionado"
        
        >
      <TagText :texto="ingrediente" :ativa="selecionado"></TagText>
    </button>
</template>

<style scoped>
.ingrediente{
    cursor: pointer;
}
</style>