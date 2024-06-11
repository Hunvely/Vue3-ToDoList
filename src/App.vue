// HTML 
<template>
  <div class="container">
    <h2>To-Do List</h2>
    <TodoSimpleForm v-on:add-todo="addTodo" />
    <hr />
    <input
      class="form-control"
      type="text"
      v-model="searchText"
      placeholder="Search"
    />
    <div v-if="!filteredTodos.length">There is nothing to display.</div>
    <TodoList
      v-bind:todos="filteredTodos"
      v-bind:todoStyle="todoStyle"
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"
    />
  </div>
</template>

// JavaScript
<script>
import { ref, computed } from "vue";
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

    const searchText = ref("");
    const filteredTodos = computed(() => {
      if (searchText.value) {
        return todos.value.filter((todo) => {
          return todo.subject.includes(searchText.value);
        });
      } else {
        return todos.value;
      }
    });

    return {
      todos,
      addTodo,
      todoStyle,
      toggleTodo,
      deleteTodo,
      searchText,
      filteredTodos,
    };
  },
};
</script>

// CSS
<style>
</style>