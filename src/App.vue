<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { id: 1, nom: 'Estudiar', completed: false },
  { id: 2, nom: 'Llegir', completed: true },
  { id: 3, nom: 'Fer esport', completed: false }
]);

const tascaNova = ref('');
const mostrarPendents = ref(false);

const tasquesTotal = computed(() => tasks.value.length);
const tasquesCompletades = computed(() => tasks.value.filter(task => task.completed).length);
const tasquesPendents = computed(() => tasks.value.filter(task => !task.completed).length);
const tasquesVisibles = computed(() =>
  mostrarPendents.value ? tasks.value.filter(task => !task.completed) : tasks.value
);

const canviarEstatTasca = (task) => {
  task.completed = !task.completed;
}

const eliminarTasca = (task) => {
  tasks.value.splice(tasks.value.indexOf(task), 1)
}

const afegirTasca = () => {
 if (!tascaNova.value.trim()) return
 tasks.value.push({
  id: tasks.value.length + 1,
  nom: tascaNova.value,
  completed: false
 });
 tascaNova.value = '';
}
</script>

<template>
  <p>Afegir una nova tasca:</p>
  <input v-model="tascaNova" type="text">
  <button v-on:click="afegirTasca">Afegir</button>
  <label>
    <input v-model="mostrarPendents" type="checkbox">
    Mostrar només pendents
  </label>
  <ul>
    <li v-for="task in tasquesVisibles" :key="task.id">
      <p v-if="task.completed">{{ task.nom }} - Completada</p>
      <p v-else="!task.completed">{{ task.nom }} - Pendent</p>
      <button v-on:click="canviarEstatTasca(task)">
        {{ task.completed ? 'Marcar com a pendent' : 'Marcar com a completada' }}
      </button>
      <button v-on:click="eliminarTasca(task)">Eliminar</button>
    </li>
  </ul>
  <p>Total: {{ tasquesTotal }} | Tasques completades: {{ tasquesCompletades }}| Tasques pendents: {{ tasquesPendents }}</p>
</template>