<template>
  <div class="home">
    <h2>Cantidad de platos: {{platosData.length}}</h2>
    <div v-for="plato in platosData" :key="plato.id">
      <p>{{plato.id}} - {{plato.nombre}}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: "Home",

  components: {
    //Todavía no utilizo componentes
  },

  mounted(){
    this.getData()
  },

  data() {
    return {
      platosData: [],
    }
  },

  methods: {
    async getData() {
      const res = await fetch("data/json/platos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.platosData = resJson.platos;//tiene que ser .platos por la estructura del JSON
    }
  }
};
</script>
