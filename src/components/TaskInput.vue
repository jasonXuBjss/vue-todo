<script setup>
import { ref, defineEmits, reactive } from 'vue';
import TaskButton from './TaskButton.vue'

const emit = defineEmits(["create-todo"])

const todoState = reactive({
    todo:"",
    invalid:null,
    errMsg:"",
});


// validation check cannot add empty string, and add task then reset the input to empty string again
const createTodo = ()=> {
        todoState.invalid = null;
        if(todoState.todo !==""){
            emit("create-todo", todoState.todo);
            todoState.todo = "";
            return;
        }
        todoState.invalid = true;
        todoState.errMsg = "can not add empty task!"
        
}

</script>


<template>
    <div class="input-wrap" :class="{}">
      <input type="text" v-model="todoState.todo" placeholder="task here...">
      <TaskButton @click="createTodo" />
    </div>
    <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
    
</template>



<style lang="scss" scoped>
    .input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41b080;
  
    &:focus-within {
      box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
        0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }
  
    input {
      width: 100%;
      padding: 8px 6px;
      border: none;
  
      &:focus {
        outline: none;
      }
    }
  
   
  }
</style>