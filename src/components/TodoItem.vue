<template>
  <div>
    <div class="row todo-item">
      <div class="d-flex col-3" v-if="!todo.editing">
        <label>
          <input type="checkbox" v-model="todo.completed" />
          <p
            class="py-3 lead todo-item todo-item-label"
            :class="{ completed: todo.completed }"
            @dblclick="editTodo(todo)"
          >
            {{ todo.title }}
          </p>
        </label>
      </div>

      <div class="my-1" v-else>
        <input
          type="text"
          class="form-control todo-item-edit"
          v-model="todo.title"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          @keyup.esc="cancelEdit(todo)"
          v-focus
        />
      </div>
      <div v-if="todo.completed && !todo.editing" class="col-5">
        <h3>Todo number {{ index + 1 }} is completed</h3>
      </div>
      <div class="col-2">
        <span @click="removeTodo(index)" class="p-3 delTodo">x</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-item",
  props: {
    author: String,
    index: {
      type: Number,
      required: true,
    },
    todo: {
      type: Object,
      required: true,
    },
  },
};
</script>
<style>
.todo-item {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.delTodo {
  text-align: center;
}
.delTodo:hover {
  color: white;
  border: 1px solid red;
  border-radius: 50%;
  background: #0ff;
}
.completed {
  background: red;
  text-decoration: line-through;
  color: blue;
}
.active {
  color: blue !important;
  background: greenyellow !important;
}
.todo-item:hover {
  background: #0f0;
  cursor: pointer;
}
</style>
