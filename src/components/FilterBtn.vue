<template>
  <div class="filterContainer">
    <div @click="openFilterMenu" class="filterBtn">
      <div class="filterBtnText">{{ currentFilter.label }}</div>
      <img
        class="filterBtnImg"
        src="../assets/select-icon.svg"
        :class="{ animated: isVisible }"
      />
    </div>
    <div class="filterListWrapper">
      <transition name="fade">
        <ul class="filterList" v-if="isVisible">
          <li
            @click="changeCurrentFilter(option.id)"
            class="filterListItem"
            v-for="option in filterOptions"
            :key="option.id"
          >
            {{ option.label }}
          </li>
        </ul>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilterBtn",
  data() {
    return {
      isVisible: false,
      currentFilter: { id: 1, label: "Все" },
      filterOptions: [
        { id: 1, label: "Все" },
        { id: 2, label: "Выполненные", value: true },
        { id: 3, label: "Невыполненные", value: false},
      ],
    };
  },
  methods: {
    openFilterMenu() {
      this.isVisible = !this.isVisible;
    },
    changeCurrentFilter(id) {
      this.currentFilter = this.filterOptions.find((el) => el.id === id);
      this.$emit("filterChanged",this.currentFilter)
      this.openFilterMenu();
    },
  },
};
</script>

<style scoped>
.filterContainer {
  user-select: none;
  position: relative;
  cursor: pointer;
  margin-left: 38px;
}

.filterBtn {
  position: relative;
  z-index: 1;
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 270px;
  height: 70px;
  background-color: #7aba3a;
  border-radius: 8px;
  padding: 0px 20px;
  transition: background-color 0.2s ease-in-out;
}

.filterListWrapper {
  position: absolute;
}

.filterBtnText,
.filterList > li {
  color: white;
  font-family: Montseratt, sans-serif;
  font-weight: 500;
  font-size: 24px;
  width: 220px;
}

ul,
li {
  margin: 0;
  padding: 0;
}

.filterBtn:hover {
  background-color: #60922d;
  transition: background-color 0.2s ease-in-out;
}
.filterList {
  position: relative;
  background-color: #99c968;
  padding-top: 10px;
  bottom: 5px;
  z-index: 0;
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
  width: 100%;
  margin-top: -10px;
}
.filterList > li {
  margin-bottom: 5px;
  cursor: pointer;
  padding: 20px 25px;
  user-select: none;
  transition: background-color 0.2s ease-in-out;
}

.filterList > li:hover {
  background-color: #60922d;
  transition: background-color 0.2s ease-in-out;
}

.filterList > li:active {
  background-color: #62bc38;
  transition: background-color 0.2s ease-in-out;
}

.filterList > li:first-child {
  padding-top: 25px;
}

.filterList > li:last-child {
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
}

.animated {
  transform: rotate(180deg);
  transition: transform 0.2s ease-in-out;
}

.filterBtnImg {
  transition: transform 0.2s ease-in-out;
}
.fade-enter-active {
  animation: fade 0.2s;
}
.fade-leave-active {
  animation: fade 0.2s reverse;
}
@keyframes fade {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
