<template>
  <div class="dropdown">
    <button class="dropbtn" @click="openDropdown()">
      {{ options[selected].value }} <i class="ri-arrow-down-s-line"></i>
    </button>
    <div class="dropdown-content" :class="{ 'dropdown-content-show': isOpen }">
      <p v-for="item in options" :key="item.id" @click="setOption(item.value)">
        {{ item.value }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "DropdownButton",
  data() {
    return {
      isOpen: false,
      selected: 2,
      options: [
        {
          id: 0,
          value: "Diario"
        },
        {
          id: 1,
          value: "Semanal"
        },
        {
          id: 2,
          value: "Mensual"
        },
        {
          id: 3,
          value: "Anual"
        }
      ]
    };
  },
  methods: {
    openDropdown() {
      this.isOpen = !this.isOpen;
    },
    setOption(value) {
      this.selected = this.options.findIndex(option => option.value === value);
      this.isOpen = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.dropbtn {
  background: black;
  border: none;
  border-radius: 12px;
  color: rgb(255, 255, 255);
  font-size: 1rem;
  font-weight: 700;
  height: 24px;
  padding: 8px 12px;
  width: 112px;
  height: fit-content;
  display: flex;
  justify-content: space-between;
  cursor: pointer;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  width: 112px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content p {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  cursor: pointer;
  margin: 0;
}

.dropdown-content p:hover {
  background-color: #f1f1f1;
}

// .dropdown:hover .dropdown-content {
//   display: block;
// }

.dropdown-content-show {
  display: block;
}

.dropdown:hover .dropbtn {
  background-color: #1e1e1e;
}
</style>