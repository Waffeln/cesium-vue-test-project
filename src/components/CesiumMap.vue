<template>
  <div class="cesium-container" id="cesiumContainer" ref="mapRef" />
</template>

<script lang="ts">
import { ref, defineComponent, onMounted } from "vue";
import * as Cesium from "cesium";

const osmBuildingsTileset = Cesium.createOsmBuildings();

osmBuildingsTileset.style = new Cesium.Cesium3DTileStyle({
  defines: {
    distanceFromComplex:
        "distance(vec2(${feature['cesium#longitude']}, ${feature['cesium#latitude']}), vec2(144.96007, -37.82249))",
  },
  color: {
    conditions: [
      ["${distanceFromComplex} > 0.010", "color('#d65c5c')"],
      ["${distanceFromComplex} > 0.006", "color('#f58971')"],
      ["${distanceFromComplex} > 0.002", "color('#f5af71')"],
      ["${distanceFromComplex} > 0.0001", "color('#f5ec71')"],
      ["true", "color('#ffffff')"],
    ],
  },
});




export default defineComponent({
  name: "CesiumMap",
  props: {
    terrainUrl: {
      default: "https://www.virtualcitymap.de/datasource-data/globalterrain_5_9",
    },
    tilesetUrl: {
      default: "https://www.virtualcitymap.de/datasource-data/f892f6af-180a-4eef-917f-5ff03c260b32/tileset.json"
    }
  },
  setup: (props) => {
    const mapRef = ref<HTMLDivElement | null>(null);
    const tileset = new Cesium.Cesium3DTileset({
      url: props.tilesetUrl,
    });

    onMounted(() => {
      const viewer = new Cesium.Viewer("cesiumContainer", {
        terrainProvider: new Cesium.CesiumTerrainProvider({url: props.terrainUrl,}),
      });

      viewer.scene.primitives.add(tileset)
      viewer.camera.flyTo({
        destination : Cesium.Cartesian3.fromDegrees( 13.404954, 52.520008, 600),
        orientation : {
          heading : Cesium.Math.toRadians(0.0),
          pitch : Cesium.Math.toRadians(-12.0),
        }
      })
      mapRef.value
    });
    return { mapRef };
  },
});
</script>

<style scoped>
#cesiumContainer {
  width: 800px;
  right: 0;
  position: absolute
}
</style>
