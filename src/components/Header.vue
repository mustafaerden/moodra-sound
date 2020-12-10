<template>
  <div
    class="header"
    :style="sidebarOpen ? { left: '260px' } : { left: '0', width: '100%' }"
  >
    <label for="toggleSidebar" @click="collapseSidebar">
      <span></span>
      <span></span>
      <span></span>
    </label>
    <h1>Moodra</h1>
  </div>
</template>

<script>
export default {
  props: ["sidebarOpen"],
  data() {
    return {};
  },
  methods: {
    collapseSidebar() {
      this.$emit("collapseSidebar");
    }
  }
};
</script>

<style scoped>
.header {
  background-color: #f2f2f2;
  height: 65px;
  padding: 5px 30px;
  display: flex;
  align-items: center;
  position: relative;
  /* left: 260px; */
  transition: 0.3s left;
  width: calc(100% - 260px);
  -moz-box-shadow: 0px 6px 14px -3px rgba(24, 31, 42, 1);
  box-shadow: 0px 6px 14px -3px rgba(24, 31, 42, 1);
}

.headerFull {
  background-color: #f2f2f2;
  height: 65px;
  padding: 5px 30px;
  display: flex;
  align-items: center;
  position: relative;
  left: 0;
  transition: 0.3s left;
  width: 100%;
  -moz-box-shadow: 0px 6px 14px -3px rgba(24, 31, 42, 1);
  box-shadow: 0px 6px 14px -3px rgba(24, 31, 42, 1);
}

.header h1 {
  color: #222c3c;
  font-size: 28px;
  letter-spacing: 2px;
  margin-left: 15px;
  text-transform: uppercase;
}

label[for="toggleSidebar"] {
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 21px;
}

label[for="toggleSidebar"] span {
  display: block;
  height: 3px;
  width: 32px;
  background-color: #222c3c;
  border-radius: 2px;
}
</style>
