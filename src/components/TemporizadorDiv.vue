<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">

    <CronometroSection :tempoEmSegundos="tempoEmSegundos"/>

<!--     <BotaoComponent @clicado="iniciar" icone="fas fa-play" texto="play" desabilitado="false"/>
    <BotaoComponent @clicado="finalizar" icone="fas fa-stop" texto="stop" desabilitado="true"/> -->

    <button class="button" @click="iniciar" :disabled="cronometroRodando">
        <span class="icon">
            <i class="fas fa-play"></i>
        </span>
        <span>play</span>
    </button>
    <button class="button" @click="finalizar" :disabled="!cronometroRodando">
        <span class="icon">
            <i class="fas fa-stop"></i>
        </span>
        <span>stop</span>
    </button>
    </div>
</template>

<script lang="ts">
// eslint-disable-next-line
import { defineComponent, initCustomFormatter } from 'vue';
import BotaoComponent from './BotaoComponent.vue';
import CronometroSection from "./CronometroSection.vue";

export default defineComponent({
    // eslint-disable-next-line
    name: 'TemporizadorDiv',
    emits: ['aoTemporizadorFinalizado'],
    components: {
    CronometroSection
},
    data () {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar () {
            this.cronometroRodando = true,
            this.cronometro = setInterval( () => {
                this.tempoEmSegundos += 1
            }, 1000 )
            console.log('iniciando');
        },
        finalizar () {
            this.cronometroRodando = false,
            clearInterval(this.cronometro),
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
            this.tempoEmSegundos = 0
        }
    }
});
</script>
