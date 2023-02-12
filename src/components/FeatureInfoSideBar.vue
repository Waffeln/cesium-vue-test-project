<template>
  <div class="SideBar">
    <div v-for="[el, value] in Object.entries(dataRef.value)">
      {{el}}: {{value}}
    </div>
  </div>
</template>

<script lang="ts">
import * as Cesium from "cesium";
import {defineComponent, ref} from "vue";

interface DataRefType {
  value: any
}

export default defineComponent({
  name: "FeatureInfoSideBar",
  props: {
    viewer:<any> {
      default: undefined
    }
  },
  mounted: function() {
    const handler = new Cesium.ScreenSpaceEventHandler(this.viewRef.scene.canvas)
    handler.setInputAction((e: any)=> {
      const feature = this.viewRef.scene.pick(e.position);
      if (feature instanceof Cesium.Cesium3DTileFeature) {
        this.dataRef.value = feature.getProperty("attributes")
      }
    }, Cesium.ScreenSpaceEventType.LEFT_CLICK)
  },
  setup: function(props) {
    const dataRef:DataRefType = ref({value: ""});
    const viewRef = ref(props.viewer)
    return {dataRef, viewRef}
  },
});
</script>

<style scoped>

.SideBar {
  width: 20%;
}

</style>