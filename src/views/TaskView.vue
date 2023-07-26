<script setup>
import { ref } from 'vue';
import TaskInput from '../components/TaskInput.vue';
import {uid} from 'uid'
import TaskItem from '../components/TaskItem.vue';

const todoList = ref([])

const createTodo = (todo)=> {
  todoList.value.push({
    //  need to change the id to connect to the server
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  })
}

const toggleTodoComplete = (todoIndex) => {
      todoList.value[todoIndex].isCompleted = !todoList.value[todoIndex].isCompleted
}

const toggleEditTodo = (todoIndex) => {
  todoList.value[todoIndex].isEditing = !todoList.value[todoIndex].isEditing
}

const updateTodo = (todoVal, todoIndex)=> {
  todoList.value[todoIndex].todo = todoVal
}

const deleteTodo = (id) => {
    todoList.value = todoList.value.filter((todo)=> {
      todo.id !== id
    })
}

</script>

<template>
  <main>
    <h1> Tasks</h1>
    <TaskInput @create-todo="createTodo"/>
    <ul class="todo-list">
      <TaskItem v-for="(todo, index) in todoList" 
        :todo="todo" :index="index" 
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
        />
    </ul>
      
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;


  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

}
</style>
