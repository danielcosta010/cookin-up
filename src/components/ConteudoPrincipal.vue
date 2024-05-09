<script lang="ts">
import Footer from './Footer.vue';
import SelecionarIngredientes from './SelecionarIngredientes.vue';
import SuaLista from './SuaLista.vue';


  export default {
    data() {
      return {
        ingredientes: [] as string[]
      }  
    }, 
    components:{ SelecionarIngredientes, SuaLista, Footer },

    methods: {
      adicionarIngredientes(ingrediente: string) {
        this.ingredientes.push(ingrediente)
      },
      removerIngrediente(ingrediente: string) {
        this.ingredientes = this.ingredientes.filter(iLista => ingrediente !== iLista)
      }
    }
  }
</script>

<template>
  <main class="conteudo-principal">
    <SuaLista :ingredientes="ingredientes"/>

    <SelecionarIngredientes 

      @adicionar-ingrediente="adicionarIngredientes"
      @remover-ingrediente="removerIngrediente"

    />

  </main>
  <footer>
    <Footer />
  </footer>
</template>

