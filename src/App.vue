<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList,
  },
};
</script>

<style>
body {
  font-family: 'Roboto', sans-serif;
  background-color: #e0f7fa;
  margin: 0;
  padding: 20px;
  color: #333;
}

#app {
  max-width: 600px;
  margin: 0 auto;
  background: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  padding: 20px;
}
</style>
