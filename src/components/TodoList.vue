<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  name: string
  status: string
}

const tasks = ref<Task[]>([
  { name: '英語の課題', status: '未完了' },
  { name: '有機化学の課題', status: '完了済み' }
])
const newTaskName = ref('')
const newTaskStatus = ref('')

const addTask = () => {
  tasks.value.push({ name: newTaskName.value, status: newTaskStatus.value })
}
</script>

<template>
  <div>
    <h2>TodoList</h2>
    <div>未完了</div>
    <ul v-for="task in tasks" :key="task.name">
      <li v-if="task.status == '未完了'">
        <div>
          {{ task.name }}
          <!-- <div>状態: {{ task.status }}</div> -->
          <button @click="task.status='完了済み'">✔️</button>
        </div>
      </li>
    </ul>
    <div>完了済み</div>
    <ul v-for="task in tasks" :key="task.name">
      <li v-if="task.status == '完了済み'">
        <div>{{ task.name }}</div>
        <!-- <div>状態: {{ task.status }}</div> -->
      </li>
    </ul>
    <div>
      <label>
        タスク
        <input v-model="newTaskName" type="text" />
      </label>
      <label>
        状態
        <input v-model="newTaskStatus" type="text" />
      </label>
      <button v-if="newTaskName!=''" @click="addTask(); newTaskName=''; newTaskStatus=''">追加</button>
      <button v-else>追加</button>
    </div>
  </div>
</template>

<style></style>