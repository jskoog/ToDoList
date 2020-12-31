/* eslint-disable no-debugger */
<template>
  <div id="app">
    <h1>This is the highest spot in the application</h1>
    <div class="form-wrapper">
      <div id="input-wrapper" style="display: inline-block">
        <input type="text" v-model="newItem.name" />
      </div>
      <div class="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="ourAddButtonWasClicked">
          Add Todo
        </button>
      </div>
      <div class="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="clearAllTodos">
          Clear All Todos
        </button>
      </div>
      <div class="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="completeAllTodos">
          Complete All Todos
        </button>
      </div>
    </div>
    <div class="todo-wrappers">
      <div v-for="todoItem in todoItems" :key="todoItem.id">
        <TodoItem
          :item="todoItem"
          :completed="todoItem.completed"
          @deleteGivenTodo="deleteGivenTodo"
          @todoItemCompleted="todoItemCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "./components/TodoItem";

export default {
  name: "App",
  components: {
    TodoItem,
  },
  data() {
    return {
      newItem: { name: "", completed: false },
      todoItems: [
        {
          id: 1,
          name: "Todo #1",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 2,
          name: "Todo #2",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 3,
          name: "Todo #3",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 4,
          name: "Todo #4",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 5,
          name: "Todo #5",
          completed: false,
          timeItWasCreated: Date.now(),
        },
      ],
    };
  },
  methods: {
    printStatus(status) {
      console.log(status);
    },
    todoItemCompleted(id) {
      // copy of the todo items array
      let toDoItemsCopy = [...this.todoItems];

      // find the index of the object in the array we want to manipulate
      const toDoItemIndex = this.todoItems.findIndex(function(todoItem) {
        return todoItem.id === id;
      });

      toDoItemsCopy[toDoItemIndex].completed = !this.todoItems[toDoItemIndex]
        .completed;

      this.todoItems = toDoItemsCopy;
    },
    completeAllTodos() {
      let newCopy = [];

      let i;
      for (i = 0; i < this.todoItems.length; i++) {
        let newObj = { ...this.todoItems[i] };
        newObj.completed = !this.todoItems[i].completed;
        newCopy[i] = newObj;
      }

      this.todoItems = newCopy;
    },
    deleteGivenTodo(id) {
      // let newTodos = [];
      // vanilla js way of removing item from array
      // let i;
      // for (i = 0; i < this.todoItems.length; i++) {
      //   if (id !== this.todoItems[i].id) {
      //     newTodos.push(this.todoItems[i]);
      //   }
      // }

      // .filter implementation of it
      let newTodos = [];

      newTodos = this.todoItems.filter(function(todoItem) {
        return todoItem.id !== id;
      });

      this.todoItems = newTodos;
    },
    ourAddButtonWasClicked() {
      const { name, completed } = this.newItem;
      
      
      // find the last id in the list
      // save that in a variable and add 1 to it

      const lastObj = this.ToDoItems.length - 1;

      const lastObjId = this.ToDoItems.indexOf(lastObj);

      this.todoItems.push({
        id: lastObjId + 1,
        name: name,
        completed: completed,
        timeItWasCreated: Date.now(),
      });
    },
    clearAllTodos() {
      this.todoItems = [];
    },
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
    this.printStatus("App.vue beforeDestroyed lifecycle hook fired");
  },
  destroyed() {
    this.printStatus("App.vue destroyed lifecycle hook fired");
  },
};
</script>

<style scoped>
#app {
  text-align: center;
}

.todo-wrappers {
  padding-top: 15px !important;
}

#input-wrapper {
  display: inline-block;
}

.todo-btn-wrapper {
  display: inline-block;
  padding-left: 5px !important;
}
</style>
