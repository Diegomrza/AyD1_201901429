<script setup>
import { ref, reactive } from "vue";

defineProps({
  msg: String,
})

const count = ref(0)

const data = reactive({
  nombre: "Diego",
  carnet: 201901429,
  curso: "Analisis y diseño de sistemas 1",
});

const showData = ref(false);

</script>

<template>
  <h1>{{ msg }}</h1>
  <hr>
  <button type="button" @click="count++">Count is {{ count }}</button>
  <hr>
  <button type="button" @click="()=> showData = !showData">Show Data</button>
  <hr>
  <div v-if="showData">
    <p>
      <strong>Nombre:</strong> {{ data.nombre }}
    </p>
    <p>
      <strong>Carnet:</strong> {{ data.carnet }}
    </p>
    <p>
      <strong>Curso:</strong> {{ data.curso }}
    </p>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

h1 {
  margin: 0;
}

button {
  margin: 0;
}

p {
  margin: 0;
}
</style>
