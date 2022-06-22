<template>
  <div id="app">
    <NavMenu></NavMenu>
    <main id="app">
        <router-view />
    </main>
    </div>
</template>

<script>
  import NavMenu from "@/components/Navbar";
  export default {
    name: "App",
    components: {
      NavMenu
    },

  };
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montseratt', sans-serif;
}

main {
    width: 100%;
    min-height: 100vh;
    overflow: hidden;
    background-color: #EEE;
    /* display: flex; */
    justify-content: center;
    align-items: center;
}

.stories {
margin-top: 100px;
max-width: 1000px;
padding: 25px;
margin: 100px auto 0 auto;
}
</style>