<template>
  <div id="app">
    <h1>This is the highest spot in the application</h1>
    <div class="form-wrapper">
      <div id="input-wrapper" style="display: inline-block">
        <input type="text" v-model="newItem.name" />
      </div>
      <div id="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="ourAddButtonWasClicked">
          Add Todo
        </button>
      </div>
      <div id="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="clearAllToDos">
          Clear All ToDos
        </button>
      </div>
      <div id="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="deleteGivenToDo">
          Delete Given ToDo
        </button>
      </div>
      <div class="todo-btn-wrapper" style="display: inline-block">
        <button v-on:click="completeAllToDos">
          Complete All ToDos
        </button>
      </div>

    </div>
    <div class="todo-wrappers">
      <div v-for="ToDoItem in ToDoItems" :key="ToDoItem.id">
        <ToDoItem 
          :item="ToDoItem" 
          :completed="ToDoItem.completed" 
          @deleteGivenToDo="deleteGivenToDo"
          @todoItemCompleted="todoItemCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue';

export default {
  name: "App",
  components: {
    ToDoItem,
  },
  data() {
    return {
      newItem: { name: "", completed: false},
      ToDoItems: 
      [
        {
          id: 1,
          name: "ToDo #1",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 2,
          name: "ToDo #2",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 3,
          name: "ToDo #3",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 4,
          name: "ToDo #4",
          completed: false,
          timeItWasCreated: Date.now(),
        },
        {
          id: 5,
          name: "ToDo #5",
          completed: false,
          timeItWasCreated: Date.now(),
        },
      ],
    };
  },
  methods: {
    printStatus(status){
      console.log(status);
    },
    todoItemCompleted(id) {
      //copy of the todo items array
      let toDoItemsCopy = [...this.ToDoItems];

      // find the index of the object in the array we want to manipulate
      const toDoItemIndex = this.ToDoItems.findIndex(function(ToDoItem) {
        return ToDoItem.id === id;
      });

      toDoItemsCopy[toDoItemIndex].completed = !this.ToDoItems[toDoItemIndex]
        .completed;

        this.ToDoItems = toDoItemsCopy;
    },
    completeAllToDos() {
      let newCopy = [];

      let i;
      for (i = 0; i < this.ToDoItems.length; i++) {
        let newObj = { ...this.ToDoItems[i] };
        newObj.completed = !this.ToDoItems[i].completed;
        newCopy[i] = newObj;
      }

      this.ToDoItems = newCopy;
    },
    deleteGivenToDo(id) {
      // let newToDos = [];
      // vanilla js way of removing item from array
      // let i;
      // for(i = 0; i < this.ToDoItems.length; i++) {
      //   if (id !== this.ToDoItems[i].id) {
      //     newToDos.push(this.ToDoItems[i]);
      //   }
      // }

      // lodash implementation of it
      let newToDos = []

      newToDos = this.ToDoItems.filter(function(ToDoItem){
        return ToDoItem.id !== id;
      });

      this.ToDoItems = newToDos;
    },
    ourAddButtonWasClicked() {
      const { name, completed } = this.newItem;
      // find the last id in the list
      // save that in a variable and add 1 to it

      const lastObj = this.ToDoItems.pop();

      const lastObjId = lastObj.id;

      this.ToDoItems.push({
        id: lastObjId + 1,
        name: name,
        completed: completed,
        timeItWasCreated: Date.now,
      });
    },
    clearAllToDos() {
      this.ToDoItems = [];
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

#todo-btn-wrapper {
  display: inline-block;

  padding-left: 5px !important;
}
</style>