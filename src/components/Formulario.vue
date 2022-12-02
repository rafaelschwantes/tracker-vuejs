<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input
                    type="text"
                    class="input"
                    placeholder="Qual tarefa você desja iniciar?"
                    v-model="descricao"
                />
            </div>
            <div class="column">
                <TemporizadorDiv @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
// eslint-disable-next-line
import { defineComponent, initCustomFormatter } from 'vue';
import TemporizadorDiv from "./TemporizadorDiv.vue";

export default defineComponent({
    // eslint-disable-next-line
    name: 'Formulario',
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorDiv
    },
    data () {
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            });

            this.descricao = '';
        }
    }
});
</script>

<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>
