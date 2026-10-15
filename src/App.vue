<template>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.nom }} - {{ task.completed ? 'Completada' : 'Pendent' }}
      <button @click="task.completed = !task.completed">
        {{ task.completed ? 'Marcar com a pendent' : 'Marcar com a completada' }}
      </button>
      <button @click="tasks.splice(tasks.indexOf(task), 1)">Eliminar</button>
    </li>
  </ul>
</template>

<script setup>
const tasks = [
  { id: 1, nom: 'Estudiar', completed: false },
  { id: 2, nom: 'Llegir', completed: true },
  { id: 3, nom: 'Fer esport', completed: false }
]
</script>
