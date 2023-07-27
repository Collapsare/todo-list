<template>
  <div id="app">
    <MyInput @addTodoItem="addTodoItem" />
    <TodoList
      :todos="todos"
      @changeFinished="changeTodoFinished"
      @itemDeleted="deleteItem"
    />
  </div>
</template>

<script>
import MyInput from "./components/MyInput.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    MyInput,
    TodoList,
  },
  data: () => {
    return {
      todos: [],
    };
  },
  methods: {
    addTodoItem(val) {
      this.todos.push({ id: this.todos.length, name: val, value: false });
    },
    changeTodoFinished(id) {
      console.log(id);
      const index = this.todos.findIndex((el) => el.id === id);
      this.todos[index].value = !this.todos[index].value;
    },
    deleteItem(id) {
      const index = this.todos.findIndex((el) => el.id === id);
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style></style>
