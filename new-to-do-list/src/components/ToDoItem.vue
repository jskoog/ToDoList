<template> 
  <div class="todo-wrapper">
    <!-- button to delete 1 ToDoItem -->
    <div class="todo-item-wrapper">
      <span
      v-on:click="toDoItemCompleted(item.id)"
      :class="`todo-item ${checkToSeeIfToDoIsCompleted(item)}`"
      >
      {{ item.name }} - {{ item.completed }} -
      {{ new Date(item.timeItWasCreated) }} 
      </span>
    </div>
    <div class="todo-delete-button-wrapper">
      <button 
        v-on:click="deleteButtonWasClicked(item.id)"
        class="todo-delete-button"
      >
        Delete {{ item.name }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoItem',
  props: ["item"],
  methods: {
    toDoItemCompleted(id) {
      this.$emit("todoItemCompleted", id);
    },
    deleteButtonWasClicked(id) {
      this.$emit("deleteGivenToDo", id);
    },
    checkToSeeIfToDoIsCompleted(item) {
      if (item.completed === true) {
        return "todo-completed";
      }
      return "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-item {
  background-color: #ffffff;
  color: darkblue;
  cursor: pointer;
}
.todo-delete-button-wrapper {
  padding-left: 16px;
  display: inline-block;
}
.todo-item-wrapper {
  display: inline-block;
}
.todo-wrapper {
  padding-top: 16px;
}
.todo-completed {
  text-decoration: line-through;
}
  </style>
