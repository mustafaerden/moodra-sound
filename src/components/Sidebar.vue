<template>
  <div
    class="sidebar"
    :style="sidebarOpen ? { left: '0' } : { left: '-260px' }"
  >
    <div id="keyInputWrapper">
      <input
        autocomplete="off"
        id="keyInput"
        type="text"
        :value="value"
        @input="updateValue($event.target.value)"
        @keyup="keyEventHandler($event.key)"
      />
      <p>Enter Key</p>
    </div>
    <ul>
      <li v-for="data in sidebarData" :key="data.id">
        <span id="idClass" className="idClass">{{ data.id }}</span>
        <span id="textClass" className="textClass">{{ data.text }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  props: ["sidebarOpen", "sidebarData", "value"],
  data() {
    return {};
  },
  methods: {
    updateValue(value) {
      this.$emit("input", value);
    },
    keyEventHandler(key) {
      this.$emit("keyEventHandler", key);
    },
  },
};
</script>

<style scoped>
.sidebar {
  background-color: #181f2a;
  width: 260px;
  /* left: 0; */
  top: 0;
  bottom: 0;
  position: fixed;
  transition: 0.3s left;
  overflow-y: scroll;
}

#keyInputWrapper {
  text-align: left;
  padding: 20px 15px;
}

#keyInputWrapper p {
  display: inline;
  color: #f2f2f2;
  margin-left: 15px;
  font-size: 18px;
}

input {
  text-align: center;
  font-size: 26px;
  color: #222c3c;
  background-color: #f2f2f2;
  height: 36px;
  width: 100px;
  padding: 5px;
  border-radius: 3px;
  border: 1px solid transparent;
  border-top: none;
  border-bottom: 1px solid #ddd;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.39), 0 -1px 1px #fff, 0 1px 0 #fff;
}

ul {
  margin: 0;
  list-style: none;
  color: #f2f2f2;
  padding-left: 0;
}

ul li {
  border-top: 1px solid #f2f2f2;
  min-width: 100%;
  padding: 15px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

ul li:hover {
  background-color: #f2f2f2;
  color: #181f2a;
}

#idClass {
  font-weight: 700;
  font-size: 20px;
  color: #ff5e5e;
  width: 13px;
}

#textClass {
  font-size: 14px;
  margin-left: 20px;
}
</style>
