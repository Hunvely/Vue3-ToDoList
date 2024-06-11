// HTML 
<template>
  <div class="container">
    <h2>To-Do List</h2>
    <TodoSimpleForm v-on:add-todo="addTodo" />
    <div v-if="!todos.length">추가된 Todo가 없습니다.</div>
    <TodoList v-bind:todos="todos" v-bind:todoStyle="todoStyle" @toggle-todo="toggleTodo" @delete-todo="deleteTodo"/>
  </div>
</template>

// JavaScript
<script>
import { ref } from "vue";
import TodoSimpleForm from "./components/TodoSimpleForm.vue";
import TodoList from "./components/TodoList.vue";
export default {
  components: {
    TodoSimpleForm,
    TodoList,
  },

  setup() {
    const todos = ref([]);
    const todoStyle = {
      textDecoration: "line-through",
      color: "gray",
    };

    const addTodo = (todo) => {
      todos.value.push(todo);
    };

    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      addTodo,
      todoStyle,
      toggleTodo,
      deleteTodo,
    };
  },
};
</script>

// CSS
<style>
</style>