<script setup lang="ts">
import { ref, onMounted } from 'vue'

const name = ref('John Doe')
const status = ref(true)
const tasks = ref(['Task one', 'Task two', 'Task three'])
const newTask = ref('asdas')

const toggleStatus = () => {
  status.value = !status.value
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()

    tasks.value = data.map((task) => task.title)
  } catch (error) {
    console.error('Error fetching tasks')
  }
})
</script>

<template>
  <header>
    <!-- Wyświetlanie zmiennych -->
    <h1 class="title">{{ name }}</h1>
    <!-- Renderowanie elementów warunkowo -->
    <p v-if="status">Użytkownik jest aktywny</p>
    <p v-else>Użytkownik jest nieaktywny</p>

    <!-- Warunkowe renderowanie z użyciem else-if -->
    <p v-if="age < 18">Użytkownik jest niepełnoletni</p>
    <p v-else-if="age >= 18 && age < 65">Użytkownik jest pełnoletni</p>
    <p v-else>Użytkownik jest na emeryturze</p>

    <section>
      <!-- Iterowanie po tanlicy i wyświetlanie elementów -->
      <h2>Zadania</h2>
      <ul>
        <li v-for="(task, index) in tasks" :key="task">
          <span>{{ task }}</span
          ><button @click="deleteTask(index)">X</button>
        </li>
      </ul>

      <!-- Przypisywanie danych do atrybutów tagów html -->
      <a :href="link" target="_blank">Link do dokumentacji</a>
    </section>

    <!-- Przypisanie funkcji do akcji submit od razu z preventDefault() -->
    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" id="newTask" name="newTask" v-model="newTask" />
      <button type="submit">Dodaj zadanie</button>
    </form>

    <section>
      <!-- Nasłuchiwanie zdarzenia click, przypisanie funkcji z methods -->
      <button v-on:click="toggleStatus">Change Status</button>
    </section>
  </header>
</template>

<style scoped>
.title {
  color: orange;
}
</style>
