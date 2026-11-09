<template>
  <main>
    <div class="columnn">
      <section class="task">
        <div class="headeer">
          <h1>Ввод</h1>
        </div>
        <input type="text" placeholder="Название задачи" v-model="taskName" @keyup.enter="addTask">
      </section>

      <section class="list">
        <div class="headeer">
          <h1>Cписок задач</h1>
        </div>

        <div v-for="task in tasks" :key="task.id" class="taskk" @click="completed(task.id)">
          {{ task.name }}
        </div>
      </section>
    </div>


    <section v-if="archived.length > 0" class="archivedd">
      <div class="headeer">
        <h2>Выполненное</h2>
      </div>

      <div v-for="task in archived" :key="task.id" class="taskk2 archivedd2">
        {{ task.name }}
      </div>
    </section>
  </main>
</template>


<style>
body {
  background-color: #0a0a0a;
  color: #ffffff;
}

main {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 20px;
  justify-content: center;
  align-items: start;
  max-width: 600px;
  min-width: 600px;
  width: 100%;
  margin: 0 auto;
}

.columnn {
  display: flex;
  flex-direction: column;
  gap: 20px;
  min-width: 0;
}

.list,
.task,
.archivedd {
  background-color: #1a1a1a;
  border-radius: 10px;
  padding: 8px 10px;
  box-shadow: 0 0 20px #ff4500;
  box-sizing: border-box;
  min-width: 0;
}

.archivedd2,
.taskk2 {
  background-color: #1a1a1a;
  border-radius: 10px;
  padding: 8px 10px;
  box-shadow: 0 0 20px #ff4500;
  box-sizing: border-box;
  min-width: 0;
  margin-bottom: 10px;
}

input {
  background-color: #212121;
  color: #ffffff;
  border: 1px solid #444444;
  border-radius: 6px;
  outline: none;

  display: block;
  box-sizing: border-box;
  padding: 10px 12px;
  width: 100%;
  margin-bottom: 20px;
}

h1,
h2 {
  color: #ff4500;
  text-shadow: 0 0 15px #ff4500;
  margin: 0;
  text-align: center;
}

.headeer {
  background-color: #2a2a2a;
  padding: 8px 10px;
  margin-bottom: 20px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 0 12px #ff4500;
  
}

.taskk {
  background-color: #2a2a2a;
  color: #ffffff;
  padding: 10px 12px;
  margin-bottom: 10px;
  border: 1px solid #444444;
  border-radius: 6px;
}
</style>


<script setup>
import { ref } from 'vue'

const taskName = ref('')
const tasks = ref([])
const archived = ref([])

function addTask() {
  const name = taskName.value.trim()

  if (name === '') {
    return
  }

  tasks.value.push({
    id: Date.now(),
    name: name
  })

  taskName.value = ''
}

function completed(id) {
  const index = tasks.value.findIndex(task => task.id === id)

  if (index === -1) {
    return
  }

  const [completed] = tasks.value.splice(index, 1)
  archived.value.push(completed)
}
</script>