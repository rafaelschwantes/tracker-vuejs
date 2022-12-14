<template>
    <header>
        <h1>
            {{ myName }}
        </h1>

        <h2>Tracker</h2>

        <button class="button" @click="alterarTema">
            {{ textoDoBotao }}
        </button>
    </header>
</template>

<script lang="ts">
//Importa as definições nativas do Vue para este componente
import { defineComponent } from 'vue';

//Eportar este componente para o projeto todo
export default defineComponent({
    //define o nome do componente
    name: 'BarraLateral',

    //declara um evento que será emidido do filho para o pai
    emits: ['aoTemaAlterado'],

    //Data é uma função que retorna um único objeto com dados que serão enviados para o frontend
    data () {
        return {
            modoEscuroAtivo: false,
            myName: 'Schwantes'
        }
    },

    // PAREI AQUI
    computed: {
        textoDoBotao () {
            if (this.modoEscuroAtivo) {
                return 'Desativar modo escuro';
            }
            return 'Ativar modo escuro';

        }
    },
    methods: {
        alterarTema () {
            console.log('Tema alterado');
            this.modoEscuroAtivo = !this.modoEscuroAtivo;
            this.$emit('aoTemaAlterado', this.modoEscuroAtivo);
        }
    }
});
</script>

<style>
/** Todo o estilo do componente */
header {
    padding: 1rem;
    background: #0d3b66;
    width: 100%;
    height: 100vh;
    text-align: center;
}

header h1 {
    font-size: 30px;
    color: #fff;
    margin-bottom: 20px;
}
header h2 {
    font-size: 20px;
    color: #fff;
    margin-bottom: 20px;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>
