<script lang="ts">
import MostrarReceitas from './MostrarReceitas.vue';
import SelecionarIngredientes from './SelecionarIngredientes.vue';
import SuaLista from './SuaLista.vue';

type Pagina = 'SelecionarIngredientes' | 'MostrarReceitas'

  export default {
    data() {
      return {
        ingredientes: [] as string[],
        conteudo: 'SelecionarIngredientes' as Pagina
      }  
    }, 
    components:{ SelecionarIngredientes, SuaLista, MostrarReceitas },

    methods: {
      adicionarIngredientes(ingrediente: string) {
        this.ingredientes.push(ingrediente)
      },
      removerIngrediente(ingrediente: string) {
        this.ingredientes = this.ingredientes.filter(iLista => ingrediente !== iLista)
      },
      navegar(pagina: Pagina) {
        this.conteudo = pagina;
      }
    }
  }
</script>

<template>
  <main class="conteudo-principal">
    
    <SuaLista :ingredientes="ingredientes"/>

    <KeepAlive include="SelecionarIngredientes">

      <SelecionarIngredientes v-if="conteudo === 'SelecionarIngredientes'"
        @adicionar-ingrediente="adicionarIngredientes"
        @remover-ingrediente="removerIngrediente"
        @buscar-receitas="navegar('MostrarReceitas')"
      />
  
      <MostrarReceitas v-else-if="conteudo ==='MostrarReceitas'"
        :ingredientes="ingredientes"
        @editar-receitas="navegar('SelecionarIngredientes')"
      />

    </KeepAlive>


  </main>
</template>

