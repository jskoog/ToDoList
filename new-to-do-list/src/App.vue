<template>
  <div id="app">
    <h1>This is the highest spot in the application</h1>
    <div class="form-wrapper">
      <div id="input-wrapper">
        <input type="text" v-model="newItem.name" />
      </div>
    
      <div id="add-todo-btn-wrapper">
      <button v-on:click="ourAddButtonWasClicked">
        Add Todo
      </button>
      </div>
      <div id="add-todo-btn-wrapper">
      <button v-on:click="clearAllToDos">
        Clear All ToDos
      </button>
      </div>
      <!-- <div id="add-todo-btn-wrapper">
      <button v-on:click="deleteOneToDo">
        Delete One ToDo
      </button>
      </div> -->

    </div>
    <div class="todo-wrappers">
      <div v-for="ToDoItem in ToDoItems" :key="ToDoItem.id">
        <ToDoItem :name="ToDoItem.name" :completed="ToDoItem.completed" />
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue';

export default {
  name: 'App',
  components: {
    ToDoItem,
  },
  data() {
    return {
      newItem: { name: "", completed: false},
      ToDoItems: 
      [
        {name:"ToDo #1", completed: false},
        {name:"ToDo #2", completed: false},
        {name:"ToDo #3", completed: false},
        {name:"ToDo #4", completed: false},
        {name:"ToDo #5", completed: false},
      ],
    };
  },
  methods: {
    printStatus(status){
      console.log(status);
    },
    ourAddButtonWasClicked() {
      // console.log(this.newItem);
      const { name, completed } = this.newItem;
      this.ToDoItems.push({
        name: name,
        completed: completed,
      });
    },
    clearAllToDos() {
      this.ToDoItems = [];
    },
    // deleteOneToDo() {
    //   this.ToDoItems.splice(this.ToDoItems.indexOf(ToDoItem), 1);
    // }
  },
  beforeCreate() {
    console.log("App.vue beforeCreate lifecycle hook fired");
  },
  created() {
    this.printStatus("App.vue created lifecycle hook fired");
  },
  beforeMount() {
    this.printStatus("App.vue beforeMount lifecycle hook fired");
  },
  mounted() {
    this.printStatus("App.vue mounted lifecycle hook fired");
  },
  beforeDestroy() {
    this.printStatus("App.vue beforeDestroy lifecycle hook fired");
  },
  destroyed() {
    this.printStatus("App.vue destroyed lifecycle hook fired");
  },
};
</script>

<style scoped>
#app {
  text-align:center
}

.todo-wrappers {
  padding-top: 15px !important;
}

#input-wrapper {
  display: inline-block;
}

#add-todo-btn-wrapper {
  display: inline-block;

  padding-left: 7px !important;
}
</style>