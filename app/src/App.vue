<template>
  <component :is="activeComponent"></component>
</template>

<script>
import TableauUserAuthentication from "./components/TableauUserAuthentication.vue";

export default {
  name: "App",
  components: {
    TableauUserAuthentication,
  },

  data() {
    return {
      uid: String,
      activeComponent: "TableauUserAuthentication",
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
