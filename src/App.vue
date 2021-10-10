<template>
  <div class="main">
    <Suspense>
      <template #default>
        <Home />
      </template>
      <template #fallback>
        <Spinner />
      </template>
    </Suspense>
  </div>
</template>

<script>
import Home from './components/home/Home.vue';
import Spinner from "./components/home/Spinner.vue";
export default {
  name: "App",
  data() {
    return {
      checkedData: [],
    };
  },
  components: {
    Home,
    Spinner
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
