<template> 
  <div>
    <!-- button to delete 1 ToDoItem -->
    <span v-on:click="toDoItemCompleted(name)" class="ToDoItem">{{name}} - {{completed}}</span>
    <span class="ToDoItem">{{ name }} - {{ completed }}</span>
    <div id="add-todo-btn-wrapper">
      <button v-on:click="ourAddButtonWasClicked">Delete {{name}}</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoItem',
  props: ["name", "completed"],
  methods: {
    toDoItemCompleted() {
      console.log("We Completed"+ name);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ToDoItem {
  background-color: #ffffff;
  color: darkblue;
}
  </style>
