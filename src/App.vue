<template>
  <div id="app">
    <Index msg="Nankunda Bright 97" />
    <TodoList />
  </div>
</template>

<script>
import Index from "./components/Index";
import TodoList from "./components/TodoList";
// import TodoList from './components/TodoList.vue';
export default {
  name: "App",
  components: {
    Index,
    TodoList,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  background: #f1f4f8;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 10px;
}
.logo {
  height: 100px;
  width: 100px;
}
</style>
