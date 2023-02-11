<template>
  <CesiumMap />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CesiumMap from "./components/CesiumMap.vue";

export default defineComponent({
  name: "App",
  components: {
    CesiumMap,
  },
});
</script>

<style>

</style>
