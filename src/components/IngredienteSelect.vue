<script>
import TagText from './TagText.vue';


export default{
    components:{
        TagText
    },
    props:{
        ingrediente:{type : String, required:true}
    },
    data() {
        return {
            selecionado:false
        }
    }
}

</script>


<template>
        <button
        class="ingrediente"
        v-on:click="selecionado=!selecionado"
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