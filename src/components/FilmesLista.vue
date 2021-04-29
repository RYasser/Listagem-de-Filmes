<template>
  <div class="row">

    <!-- coluna 1 -->
    <div class="col-8">

      <h2>Filmes</h2>

      <ul class="list-group list-group-flush">
        <!-- Cria dinamicamente novo itêm de filme de acordo com o conteúdo do array de objetos filmes -->
        <FilmesListaIten v-for="filme in filmes" 
        :key="filme.id" 
        :filme="filme" 
        :class="aplicarClassAtiva(filme)"
        @selecionarFilme="filmeSelecionado = $event"/>

      </ul>
    </div>

    <!-- coluna 2 -->
    <div class="col-4">

      <FilmesListaItenInfo v-if="!editar" @editarFilme="editarFilme"/>

      <FilmesListaItenEditar v-else :filme="filmeSelecionado"/>

    </div>

  </div>
</template>

<script>

import FilmesListaIten from './FilmesListaIten.vue'
import FilmesListaItenInfo from './FilmesListaItenInfo.vue'
import FilmesListaItenEditar from './FilmesListaItenEditar'
import { eventBus } from './../main'

export default {
  data() {
    return {
      filmes: [
        { id: 1, titulo: 'Os Vingadores: Guerra Infinita', ano: '2018'},
        { id: 2, titulo: 'Capitã Marvel', ano: '2019' },
        { id: 3, titulo: 'Homem Formiga e a Vespa', ano: '2017' }
      ],
      filmeSelecionado: undefined,
      editar: false
    }    
  },
  components: {
    FilmesListaIten,
    FilmesListaItenInfo,
    FilmesListaItenEditar
  },
  methods: {
    aplicarClassAtiva(filmeIterado) {
      return {
        active: this.filmeSelecionado && this.filmeSelecionado.id === filmeIterado.id
      }
    },
    editarFilme() {
      this.editar = true
  
    },
    atualizarFilme(filmeAtualizado) {
      const indice = this.filmes.findIndex(filme => filme.id === filmeAtualizado.id)
      this.filmes.splice(indice, 1, filmeAtualizado)
      this.filmeSelecionado = undefined
      this.editar = false
    }
  },
  created() {
    eventBus.$on('atualizarFilme', this.atualizarFilme)
  }
}
</script>
