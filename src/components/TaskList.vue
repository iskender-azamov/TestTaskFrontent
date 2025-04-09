<template>
  <div>
    <div v-for="task in tasks" :key="task.id">
      <label>
        <input type="checkbox" v-model="task.done" @change="saveToLocalStorage" />
        <span :style="{ textDecoration: task.done ? 'line-through' : 'none' }">
          {{ task.title }}
        </span>
      </label>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface Task {
  id: number
  title: string
  done: boolean
}

const tasks = ref<Task[]>([])

const loadFromLocalStorage = () => {
  const saved = localStorage.getItem('tasks')
  if (saved) {
    tasks.value = JSON.parse(saved)
  }
}

const saveToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

const fetchTasks = async () => {
  const res = await fetch('/tasks.json')
  const data: Task[] = await res.json()
  tasks.value = data
  saveToLocalStorage()
}

onMounted(() => {
  loadFromLocalStorage()
  if (!tasks.value.length) fetchTasks()
})
</script>
