<template id='app'>
  <div class="Container">
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator";
export default {
  name: "App",
  components: {
    Calculator,
  },
};
</script>

<style scoped>
div.Container {
  display: flex;
  align-content: center;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>