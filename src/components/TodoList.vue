<template>
  <div class="container">
    <div class="wrapper bg-light form-group">
      <div class="form-group">
        <input
          type="text"
          class="form-control todo-input"
          placeholder="What next needs to be done..."
          v-model="newTodo"
          @keyup.enter="addTodo"
        />
      </div>

      <TodoItem
        author="Nintey Seven"
        v-for="(todo, index) in todosFiltered"
        :key="index"
        :todo="todo"
        :index="index"
      />
    </div>
    <div class="row border-top">
      <div class="col-5">
        <label
          ><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos" />Check
          All</label
        >
      </div>

      <div class="col-5">{{ remaining }} Tasks Left</div>
    </div>
    <div class="row">
      <div class="col-8 d-flex">
        <button :class="{ active: filter == 'all' }" @click="filter = 'all'" class="btn">
          All
        </button>
        <button
          :class="{ active: filter == 'active' }"
          @click="filter = 'active'"
          class="btn"
        >
          Active
        </button>
        <button
          :class="{ active: filter == 'completed' }"
          @click="filter = 'completed'"
          class="btn"
        >
          Completed
        </button>
      </div>
      <div class="col-2">
        <button class="btn btn-danger" v-if="showClearCompleted" @click="clearCompleted">
          Clear Completed
        </button>
      </div>
      <Cats name="tom cat" />
    </div>
  </div>
</template>
<script>
import Cats from "./Cats";
import TodoItem from "./TodoItem";
export default {
  name: "TodoList",
  components: {
    TodoItem,
    Cats,
  },
  data() {
    return {
      idForTodo: 4,
      newTodo: "",
      beforeEditCache: "",
      filter: "all",
      todos: [
        {
          id: 1,
          title: "Master Vue",
          completed: false,
          editing: false,
        },
        {
          id: 2,
          title: "Finish Laravel",
          completed: true,
          editing: false,
        },
        {
          id: 3,
          title: "Start React natve",
          completed: false,
          editing: false,
        },
      ],
    };
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },
  computed: {
    todosFiltered() {
      if (this.filter == "all") {
        return this.todos;
      } else if (this.filter == "active") {
        return this.todos.filter((todo) => !todo.completed);
      } else if (this.filter == "completed") {
        return this.todos.filter((todo) => todo.completed);
      }
      return this.todos;
    },
    anyRemaining() {
      return this.remaining != 0;
    },
    remaining() {
      return this.todos.filter((todo) => !todo.completed).length;
      // return this.todos.completed.length;
    },
    showClearCompleted() {
      return this.todos.filter((todo) => todo.completed).length > 0;
    },
  },
  methods: {
    checkAllTodos(event) {
      this.todos.forEach((todo) => (todo.completed = event.target.checked));
      // console.log(event.target);
    },
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false,
      });
      this.newTodo = "";
      this.idForTodo++;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    //
    // updateTodo(index) {
    //   this.todos.splice(index, 1, {
    //     id: 4,
    //     title: "newTodo",
    //     completed: false,
    //   });
    // },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
      this.beforeEditCache = "";
    },
    clearCompleted() {
      this.todos = this.todos.filter((todo) => !todo.completed);
    },
  },
};
</script>
<style>
.todo {
  padding: 10px;
}

.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
