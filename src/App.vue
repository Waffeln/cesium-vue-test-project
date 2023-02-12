<template>
  <div class="cesium-container" id="cesiumContainer" ref="mapRef" />
  <CesiumMap />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CesiumMap from "./components/CesiumMap.vue";
import FeatureInfoSideBar from "./components/FeatureInfoSideBar.vue";

export default defineComponent({
  name: "App",
  components: {
    FeatureInfoSideBar,
    CesiumMap,
  },
});
</script>

<style>
#cesiumContainer {
  width: 80%;
  right: 0;
  position: absolute
}
</style>
