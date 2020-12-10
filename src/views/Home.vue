<template>
  <div class="home">
    <router-link class="linkButton" to="/kathy">Go To Kathy</router-link>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style scoped>
.home {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.linkButton {
  text-decoration: none;
  background: #ff5e5e;
  padding: 10px 25px;
  color: #fff;
  border-radius: 5px;
}
</style>
