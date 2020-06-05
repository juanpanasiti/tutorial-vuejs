<template>
  <div id="app">
    <navigation-bar />
    <router-view/>
  </div>
</template>

<script>
import Navigation from "@/components/bootstrap/Navigation.vue"
export default {
  components:{
    "navigation-bar": Navigation
  }
}
</script>
