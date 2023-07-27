<template>
  <form class="input" @submit="cancelSubmit">
    <input type="text" class="input-text" v-model="todoName" />
    <button class="input-btn" @click="addTodoItem">+</button>
  </form>
</template>

<script>
export default {
  name: "MyInput",
  data() {
    return {
      todoName: "",
    };
  },
  methods: {
    addTodoItem() {
      this.$emit("addTodoItem", this.todoName);
    },
    cancelSubmit(event) {
      event.preventDefault();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input {
  height: 70px;
  width: 422px;
  position: relative;
}
.input-text {
  box-sizing: border-box;
  border: 1px solid #d3d3d3;
  border-radius: 8px;
  height: 70px;
  width: 422px;
  font-size: 24px;
  padding: 0 74px 0 10px;
}

.input-btn {
  width: 48px;
  height: 48px;
  border-radius: 8px;
  background: #7aba3a;

  display: flex;
  align-items: center;
  justify-content: center;

  color: #fff;
  font-size: 42px;
  font-weight: bold;
  font-family: Inter, sans-serif;

  position: absolute;
  bottom: 11px;
  right: 16px;
  cursor: pointer;
  border: none;
}
</style>
