<template>
    <li class="list-group-item">
        <span>  {{ filme.titulo }} | {{ filme.ano }} </span>
        <button @click="selecionar" class="btn btn-secondary float-right">Selecionar</button>
    </li>
</template>

<script>
import { eventBus } from './../main' 

export default {
    props: {
        filme: {
            type: Object,
            required: true
        }
    },
    methods: {
        selecionar() {
            // Passa o objeto de filmes para o lista aplicar a classe selecionado
            this.$emit('selecionarFilme', this.filme)
            // Passando o objeto de filmes para o info
            eventBus.selecionarFilme(this.filme)
        }
    }
}
</script>
