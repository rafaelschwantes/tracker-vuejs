<template>
  <main class="columns ls-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <TarefaComponent v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        <BoxComponent v-if="listaEstaVazia">Ainda não houve registro de tarefas.</BoxComponent>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import Formulario from './components/Formulario.vue';
import TarefaComponent from './components/TarefaComponent.vue';
import BoxComponent from "./components/BoxComponent.vue";
import ITarefa from './interfaces/ITarefa';

export default defineComponent({
  name: 'App',
  emits: ['aoSalvarTarefa'],
  components: {
    BarraLateral,
    Formulario,
    BoxComponent,
    TarefaComponent
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },
  computed: {
    listaEstaVazia () :boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa (tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },

    trocarTema (modoEscuroAtivo :boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo
    }
  }
});
</script>

<style>
.lista {
    padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #000;
  --texto-primario: #fff;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
