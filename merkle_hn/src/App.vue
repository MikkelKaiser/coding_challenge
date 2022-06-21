<template>
  <div id="app">
    <NavMenu></NavMenu>
    <router-view />
  </div>
</template>

<script>
  import NavMenu from "@/components/Navbar";
  export default {
    name: "App",
    components: {
      NavMenu
    }
  };
</script>

<style></style>