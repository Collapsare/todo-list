<template>
  <div class="todoList">
    <TodoListItem
      v-for="item in todos"
      :key="item.id"
      :item="item"
      class="todoItem"
      @changeFinished="changeTodoFinished"
      @itemDeleted="deleteItem"
    />
  </div>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";

export default {
  name: "TodoList",
  components: {
    TodoListItem,
  },
  props: {
    todos: {
      required: true,
      default: () => [],
      type: Array,
    },
  },
  methods: {
    changeTodoFinished(id) {
      this.$emit("changeFinished", id);
    },
    deleteItem(id) {
      this.$emit("itemDeleted", id);
    },
  },
};
</script>

<style>
.todoList {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
