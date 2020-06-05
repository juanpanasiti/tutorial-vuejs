<template>
  <div class="home">
    <h2>Cantidad de platos: {{ platosData.length }}</h2>

    <div class="row">
      <div v-for="plato in platosData" :key="plato.id" class="col-4">
        <plato-item :platoParam="plato" />
      </div>
    </div>
  </div>
</template>

<script>
import PlatoCard from "@/components/PlatoCard.vue";
export default {
  name: "Home",

  components: {
    "plato-item": PlatoCard,
  },

  mounted() {
    this.getData();
  },

  data() {
    return {
      platosData: [],
    };
  },

  methods: {
    async getData() {
      const res = await fetch("data/json/platos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.platosData = resJson.platos; //tiene que ser .platos por la estructura del JSON
    },
  },
};
</script>
