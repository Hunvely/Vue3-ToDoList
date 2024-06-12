<template>
  <div v-for="(todo, index) in todos" v-bind:key="todo.id" class="card mt-2">
    <div class="card-body p-2 d-flex align-items-center">
      <div class="form-check flex-grow-1">
        <input
          class="form-check-input"
          type="checkbox"
          v-bind:value="todo.completed"
          @change="toggleTodo(index)"
        />
        <label
          class="form-check-label"
          v-bind:style="todo.completed ? todoStyle : {}"
        >
          {{ todo.subject }}
        </label>
      </div>
      <button class="btn btn-primary btn-sm">Update</button>
      <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">
        Delete
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
    todoStyle: {
      type: Object,
      required: true,
    },
  },
  emits: ["toggle-todo", "delete-todo"],
  setup(props, { emit }) {
    const toggleTodo = (index) => {
      emit("toggle-todo", index);
    };

    const deleteTodo = (index) => {
      emit("delete-todo", index);
    };

    return {
      toggleTodo,
      deleteTodo,
    };
  },
};
</script>

<style>
</style>