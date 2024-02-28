<script> 
export default {
  data() {
    return {
      contador: 0,
    };
  },
  methods: {
    incrementar() {
      this.contador++;
    },
    decrementar() {
      if (this.contador > 0) {
        this.contador--;
      }
    },
    reiniciar() {
      this.contador = 0;
    },
  },
};
</script>

<template>
<div>
  <h1>Contador</h1>
  <p> {{ contador }} </p>
  <button @click="incrementar">Incrementar</button>
  <button @click="decrementar">Decrementar</button>
  <button @click="reiniciar">Reiniciar</button>
</div>
</template>