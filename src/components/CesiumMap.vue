<template>
  <FeatureInfoSideBar :viewer="this.viewerRef" />
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import * as Cesium from "cesium";
import FeatureInfoSideBar from "./FeatureInfoSideBar.vue";

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
  components: {
    FeatureInfoSideBar
  },
  setup: function(props) {

    const tileset = new Cesium.Cesium3DTileset({
      url: props.tilesetUrl,
    });
    tileset.style = new Cesium.Cesium3DTileStyle({
      color: {
        conditions : [
          ['true', 'color("green")']
        ]
      }
    })

    const viewer = new Cesium.Viewer("cesiumContainer", {
      terrainProvider: new Cesium.CesiumTerrainProvider({
        url: props.terrainUrl
      })
    });

    viewer.scene.primitives.add(tileset);
    viewer.camera.flyTo({
      destination : Cesium.Cartesian3.fromDegrees( 13.404954, 52.520008, 200),
      orientation : {
        heading : Cesium.Math.toRadians(0.0),
        pitch : Cesium.Math.toRadians(-40.0),
      }
    })

    const viewerRef = ref(viewer);

    return {viewerRef}
  },
});
</script>

<style scoped>
</style>
