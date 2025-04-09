<template>
  <main class="container">
    <h1>🧪 Тестовое задание</h1>
    <TaskList />
  </main>
</template>

<script setup lang="ts">
import TaskList from './components/TaskList.vue'
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}
</style>
