<template>
  <div class="todoItem">
    <input
      class="todoItemCheckbox"
      type="checkbox"
      :id="item.id"
      :value="item.value"
      @input="changeTodoFinished(item.id)"
    />
    <label class="todoItemText" :for="item.id">{{ item.name }}</label>
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
  display: flex;
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
  margin-right: 20px;
}

.todoItemCheckbox:checked + label::before {
  border-color: #7aba3a;
  background-color: #7aba3a;
  background-image: url(../assets/checkbox-checked-icon.svg);
}

.todoItemCheckbox:checked + label {
  text-decoration: line-through;
}

.todoItem {
  display: flex;
  justify-content: space-between;
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
.deleteBtn {
  width: 50px;
  height: 50px;

  border-radius: 5px;
  border: none;

  background-color: #f07070;
  background-image: url(../assets/delete-btn-icon.svg);
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}
</style>
