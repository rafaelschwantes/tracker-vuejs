<template>
    <BoxComponent>
        <div class="columns">
            <div class="column is-7">
                {{tarefa.descricao || 'Tarefa sem descrição'}}
            </div>
            <div class="column">
                <CronometroSection :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxComponent>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import CronometroSection from "./CronometroSection.vue";
import ITarefa from "../interfaces/ITarefa";
import BoxComponent from "../components/BoxComponent.vue";

export default defineComponent({
    name: 'TarefaComponent',
    components: {
        CronometroSection,
        BoxComponent
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
});
</script>
