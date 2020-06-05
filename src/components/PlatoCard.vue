<template>
  <div>
    <b-card
      :title="platoParam.nombre"
      :img-src="'/data/images/' + platoParam.imagenPath"
      :img-alt="'Imagen de ' + platoParam.nombre"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
    >
      <b-card-text>
        <h3>$ {{platoParam.precio}}</h3>
        
        <span v-if="platoParam.rubro === 'Bebidas'">Desc. 20% comprando 2 o más</span>

        <h5>Ingredientes:</h5>
        <p>
            <ul>
                <li v-for="(ingrediente,i) in platoParam.ingredientes" :key="i">
                    {{ingrediente}}
                </li>
            </ul>
        </p>
        
      </b-card-text>

      <b-button href="#" variant="primary">Ver detalle</b-button>
    </b-card>
  </div>
</template>

<script>
export default {
  props: ["platoParam"],
};
</script>
