<template>
  <div id="app">
    <button v-for="n in markers" :key="n.id" @click="onClick(n)">
      #{{ n.id }}
    </button>
    <yandex-map
      ref="map"
      :coords="[55.72, 37.65]"
      zoom="10"
      style="width: 100%; height: 600px"
      :controls="[]"
    >
      <ymap-marker
        v-for="n in markers"
        :key="n.id"
        :marker-id="n.id"
        marker-type="placemark"
        :coords="n.coord"
        :balloon="{ body: n.text }"
      ></ymap-marker>
    </yandex-map>
  </div>
</template>

<script>
import { yandexMap, ymapMarker } from "vue-yandex-maps";

export default {
  name: "App",
  components: {
    yandexMap,
    ymapMarker,
  },
  data() {
    return {
      markers: [
        { coord: [55.8, 37.4], text: "hello, world!!" },
        { coord: [55.6, 37.5], text: "fuck the world" },
        { coord: [55.7, 37.7], text: "fuck everything" },
      ].map((n, i) => ({ ...n, id: i + 1 })),
    };
  },
  methods: {
    onClick(m) {
      this.$refs.map.myMap.balloon.open(m.coord, m.text);
    },
  },
};
</script>

<style>
</style>
