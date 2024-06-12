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
    <div class="emptyContainer" v-if="!filteredTodos.length">
      <div class="empty">There are no items displayed in the To-Do list..</div>
    </div>
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
h2 {
  text-align: center;
  font-family: "Arial", sans-serif;
  font-size: 2.5em;
  color: #007bff;
  background-color: #f8f9fa;
  border: 2px solid #007bff;
  border-radius: 10px;
  padding: 10px 20px;
  margin-top: 20px;
  margin-bottom: 20px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.1);
}
.emptyContainer {
  text-align: center;
}
.empty {
  display: inline-block;
  font-family: "Arial", sans-serif;
  font-size: 1.1em;
  margin-top: 15px;
  color: #dc3545;
  background-color: #f8d7da;
  border: 2px solid #dc3545;
  border-radius: 10px;
  padding: 10px 20px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
</style>