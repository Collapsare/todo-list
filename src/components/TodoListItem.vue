<template>
  <div class="todoItem">
    <input
      type="checkbox"
      id="checkbox"
      class="todoItemCheckbox"
      :value="item.value"
      @input="changeTodoFinished(item.id)"
    />
    <label for="checkbox" class="todoItemText">{{ item.name }}</label>
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

<style scoped>
.todoItemCheckbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}
.todoItemCheckbox + label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}
.todoItemCheckbox + label::before {
  content: "";
  display: block;
  width: 50px;
  height: 50px;
  border: 1px solid black;
  border-radius: 50%;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 70% 70%;
}

.todoItemCheckbox:checked + label::before {
  border-color: #7aba3a;
  background-color: #7aba3a;
  background-image: url(../assets/Vector.svg);
}

.todoItem {
  width: 750px;
  height: 80px;
  box-sizing: border-box;
  padding: 15px;
  background-color: #f9f9fa;
  border-radius: 4px;
}
.todoItemText {
  font-size: 24px;
  font-family: Montserrat, sans-serif;
}
</style>
