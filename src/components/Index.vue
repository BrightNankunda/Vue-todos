<template>
  <div>
    <h2>Vue Todo App</h2>
    <h3>{{ msg }}</h3>
    <b-icon icon="arrow-up"></b-icon>
  </div>
</template>
<script>
export default {
  name: "Index",
  props: {
    msg: String,
  },
};
</script>
