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

      <FilmesListaItenInfo/>
      <!-- :filme="filmeSelecionado" -->

    </div>

  </div>
</template>

<script>

import FilmesListaIten from './FilmesListaIten.vue'
import FilmesListaItenInfo from './FilmesListaItenInfo.vue'

export default {
  data() {
    return {
      filmes: [
        { id: 1, titulo: 'Os Vingadores: Guerra Infinita', ano: '2018'},
        { id: 2, titulo: 'Capitã Marvel', ano: '2019' },
        { id: 3, titulo: 'Homem Formiga e a Vespa', ano: '2017' }
      ],
      filmeSelecionado: undefined
    }    
  },
  components: {
    FilmesListaIten,
    FilmesListaItenInfo
  },
  methods: {
    aplicarClassAtiva(filmeIterado) {
      return {
        active: this.filmeSelecionado && this.filmeSelecionado.id === filmeIterado.id
      }
    }
  }
}
</script>
