<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { id: 1, nom: 'Estudiar', completed: false },
  { id: 2, nom: 'Llegir', completed: true },
  { id: 3, nom: 'Fer esport', completed: false }
]);

const tascaNova = ref('');

const tasquesTotal = computed(() => tasks.value.length);
const tasquesCompletades = computed(() => tasks.value.filter(task => task.completed).length);
const tasquesPendents = computed(() => tasks.value.filter(task => !task.completed).length);

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
  <button v-on:click="mostrarPendents">Mostrar només pendents</button>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.nom }} - {{ task.completed ? 'Completada' : 'Pendent' }}
      <button v-on:click="canviarEstatTasca(task)">
        {{ task.completed ? 'Marcar com a pendent' : 'Marcar com a completada' }}
      </button>
      <button v-on:click="eliminarTasca(task)">Eliminar</button>
    </li>
  </ul>
  <p>Total: {{ tasquesTotal }} | Tasques completades: {{ tasquesCompletades }}| Tasques pendents: {{ tasquesPendents }}</p>
</template>