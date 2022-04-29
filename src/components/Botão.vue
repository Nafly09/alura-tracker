<template>
  <button class="button" @click="clicado" :disabled="desabilitado">
    <span class="icon">
      <i :class="icon"></i>
    </span>
    <span>{{ text }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Button",
  emits: ["clicado"],
  props: {
    desabilitado: {
      type: Boolean,
    },
    icon: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
  },
  methods: {
    clicado(): void {
      this.$emit("clicado");
    },
  },
});
</script>
