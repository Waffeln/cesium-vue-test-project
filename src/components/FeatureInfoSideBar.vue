<template>
  <div class="SideBar">
    <div v-for="[el, value] in Object.entries(dataRef.value)">
      {{el}}: {{value}}
    </div>
  </div>
</template>

<script lang="ts">
import * as Cesium from "cesium";
import {defineComponent, ref, UnwrapRef} from "vue";

interface DataRefType {
  value: any
}

export default defineComponent({
  name: "FeatureInfoSideBar",
  props: {
    viewer: {
      type: Object as () => UnwrapRef<Cesium.Viewer>
    }
  },
  mounted: function() {
    const handler = new Cesium.ScreenSpaceEventHandler(this.viewRef?.scene.canvas)
    handler.setInputAction((e: Cesium.ScreenSpaceEventHandler.PositionedEvent)=> {
      console.log(this.viewRef?.selectedEntity?.name)
      const feature = this.viewRef?.scene.pick(e.position);
      if (feature instanceof Cesium.Cesium3DTileFeature) {
        this.dataRef.value = feature.getProperty("attributes")
      }
    }, Cesium.ScreenSpaceEventType.LEFT_CLICK)
  },
  setup: function(props) {
    const dataRef:DataRefType = ref({value: ""});
    const viewRef = ref(props.viewer as UnwrapRef<Cesium.Viewer>)
    return {dataRef, viewRef}
  },
});
</script>

<style scoped>

.SideBar {
  width: 20%;
}

</style>