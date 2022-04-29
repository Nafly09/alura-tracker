<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Cronometro :tempoEmSegundos="tempoEmSegundos" />
    <Button
      @clicado="iniciar"
      icon="fas fa-play"
      text="Start"
      :desabilitado="cronometroRodando"
    />
    <Button
      @clicado="finalizar"
      icon="fas fa-stop"
      text="Stop"
      :desabilitado="!cronometroRodando"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Cronometro from "./Cronometro.vue";
import Button from "./Botão.vue";

export default defineComponent({
  name: "Temporizador",
  emits: ["aoTemporizadorFinalizado"],
  components: {
    Cronometro,
    Button,
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciar() {
      // começar a contagem
      // 1 seg = 1000 ms
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizar() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>
