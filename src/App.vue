<template>
  <div id="app">
    <MyInput @addTodoItem="addTodoItem" />
    <FilterBtn @filterChanged="filterTodos" />
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
      currentFilter: {},
    };
  },
  methods: {
    addTodoItem(val) {
      this.todos = this.backNewItem(val);
      if (this.currentFilter) this.filterTodos(this.currentFilter);
    },
    changeTodoFinished(val) {
      this.todos = this.backChangeItem(val);
      if (this.currentFilter) this.filterTodos(this.currentFilter);
    },
    deleteItem(val) {
      this.todos = this.backRemoveItem(val);
      if (this.currentFilter) this.filterTodos(this.currentFilter);
    },
    backNewItem(item) {
      const data = this.getData();
      localStorage.setItem(
        "data",
        JSON.stringify([{ id: data.length, name: item, value: false }, ...data])
      );

      return this.getData();
    },
    backRemoveItem(item) {
      const data = this.getData();
      const index = data.findIndex((el) => el.id === item.id);

      if (index !== -1) {
        data.splice(index, 1);
        localStorage.setItem("data", JSON.stringify(data));
      }

      return this.getData();
    },
    backChangeItem(item) {
      const data = this.getData();
      const index = data.findIndex((el) => el.id === item.id);

      if (index !== -1) {
        data[index].value = !data[index].value;
        localStorage.setItem("data", JSON.stringify(data));
      }

      return this.getData();
    },
    getData() {
      return JSON.parse(localStorage.getItem("data")) || [];
    },
    filterTodos(val) {
      this.currentFilter = val;
      this.todos = this.getData().filter(
        (el) => val.value === undefined || el.value === val.value
      );
    },
  },

  created() {
    const data = this.getData();

    if (data) {
      this.todos = data;
    }
  },
};
</script>

<style>
#app {
  width: 800px;
  margin: 0 auto;
  margin-top: 100px;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
</style>
