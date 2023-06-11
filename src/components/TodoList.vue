<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  name: string
  status: string
  limit: string
}

const tasks = ref<Task[]>([
  { name: '英語の課題', status: '未完了', limit: '6/12' },
  { name: '有機化学の課題', status: '完了済み', limit: '' }
])

const newTaskName = ref('')
const newTaskStatus = ref('未完了')
const newTaskLimit = ref('')

const addTask = () => {
  tasks.value.push({ name: newTaskName.value, status: newTaskStatus.value, limit: newTaskLimit.value})
}

const duplicateCheck = (name_:string) => {
  let flag = false
  for (let i = 0; i < tasks.value.length; ++i){
    if (name_==tasks.value[i].name){
      flag = true
    }
  }
  return flag
}

const deleteTask = (x:number) => {
  tasks.value.splice(x,1)
}
</script>

<template>
  <div>
    <h2>TodoList</h2>
    <h3>未完了</h3>
      <div v-if="tasks.filter(t => t.status == '未完了').length==0">未完了のタスクはありません</div>
      <ul v-for="(task, index) in tasks" :key="task.name">
        <li v-if="task.status=='未完了'">
          <div v-if="task.limit == ''">
            {{ task.name }}（期限：なるべく早く）
            <button @click="task.status='完了済み' ">✔️</button>
            <button @click="deleteTask(index)">削除</button>
          </div>
          <div v-else>
            {{ task.name }}（期限：{{ task.limit }}）
            <button @click="task.status='完了済み' ">✔️</button>
            <button @click="deleteTask(index)">削除</button>
          </div>
        </li>
      </ul>
    <h3>完了済み</h3>
      <ul v-for="(task, index) in tasks" :key="task.name">
        <li v-if="task.status=='完了済み'">
          <div>
            {{ task.name }}
            <button @click="deleteTask(index)">削除</button>
          </div>
        </li>
      </ul>
      <label>
        タスク内容
        <input v-model="newTaskName" type="text" placeholder="タスクをここに入力" />
        <div v-if="duplicateCheck(newTaskName)">⚠️このタスクはすでに追加されています</div>
      </label>
    <div>
      <label>
        期限
        <input v-model="newTaskLimit" type="text" placeholder="期限をここに入力" />
      </label>
      <button v-if="duplicateCheck(newTaskName)">追加</button>
      <button v-else-if="newTaskName!=''" @click="addTask(); newTaskName=''">追加</button>
      <button v-else>追加</button>
    </div>
  </div>
</template>

<style></style>