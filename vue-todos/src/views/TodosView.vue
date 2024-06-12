<script setup>
import { ref } from 'vue'
import {uid} from "uid";
import { Icon } from "@iconify/vue";
import TodoCreator from '../components/TodoCreator.vue'
import TodoItem from '../components/TodoItem.vue'

const todoList = ref([]);

const createTodo = (todo) =>{
  todoList.value.push({
    id: uid(),
    todo: todo,
    isCompleted: null,
    isEditing: null,
  })
}

const toggleTodoComplete = (todoPosition) =>{
  todoList.value[todoPosition].isComplete = !todoList.value[todoPosition].isComplete;
}

const toggleEditTodo = (todoPosition) =>{
  todoList.value[todoPosition].isEditing = !todoList.value[todoPosition].isEditing;
}

const updateTodo = (todoVal, todoPosition) => {
  todoList.value[todoPosition].todo = todoVal;
}
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo"/>
    <ul class="todo-list">
      <TodoItem 
        v-for="(todo, index) in todoList" 
        :todo="todo" :index="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        />
    </ul>
    <p v-if="todoList.length == 0" class="todos-msg">
      <span>you have no todos</span>
    </p>
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

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
