<template>
  <div id="app">
    <navigation-bar />
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
import Navigation from "@/components/bootstrap/Navigation.vue";
export default {
  components: {
    "navigation-bar": Navigation,
  },
};
</script>
