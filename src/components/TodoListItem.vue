<template>
  <div>
    <label class="todoItemText">
      <input
        type="checkbox"
        :value="item.value"
        @input="changeTodoFinished(item.id)"
      />
      <span>{{ item.name }}</span>
    </label>
    <button class="deleteBtn" @click="deleteItem(item.id)"></button>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props: {
    item: {
      required: true,
      default: () => {},
      type: Object,
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

<style scoped></style>
