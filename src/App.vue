<template>
  <div id="app">
    <MyInput @addTodoItem="addTodoItem" />
    <FilterBtn/>
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
import FilterBtn from "./components/FilterBtn.vue";

export default {
  name: "App",
  components: {
    MyInput,
    TodoList,
    FilterBtn,
  },
  data: () => {
    return {
      todos: [],
    };
  },
  methods: {
    addTodoItem(val) {
      this.todos.push({ id: this.todos.length, name: val, value: false });
      this.saveAllData();
    },
    changeTodoFinished(id) {
      const index = this.todos.findIndex((el) => el.id === id);
      this.todos[index].value = !this.todos[index].value;
      this.saveAllData();
    },
    deleteItem(id) {
      const index = this.todos.findIndex((el) => el.id === id);
      this.todos.splice(index, 1);
      this.saveAllData();
    },
    saveAllData() {
      localStorage.setItem('data', JSON.stringify(this.todos))
    },
    getData() {
      return JSON.parse(localStorage.getItem('data'))
    }
  },
  created() {
    const data = this.getData();
    if (data) this.todos = data;
  }
};
</script>

<style></style>
