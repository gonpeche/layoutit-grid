<template>
  <div class="area-props">
    <button v-if="area.grid" @click="addImplicitArea">Add Implicit Area</button>
    <FlexOptions v-if="area.flex" :flex="area.flex" />
    <GridOptions v-if="area.grid" :grid="area.grid" />
  </div>
</template>

<script setup="props">
export { default as FlexOptions } from './FlexOptions.vue'
export { default as GridOptions } from './GridOptions.vue'

import { ref, computed } from 'vue'
import { createAreaState } from '../../store'
export { currentArea, currentView } from '../../store.js'
export { gridRegionToGridArea } from '../../utils.js'

export default {
  name: 'AreaProps',
  props: {
    area: { type: Object, required: true },
  },
}

export const currentGrid = computed(() => props.area.grid)
export const currentFlex = computed(() => props.area.flex)

const counter = ref(1)
export function addImplicitArea() {
  props.area.grid.areas.push(
    createAreaState({
      name: 'a' + counter.value++,
      parent: props.area,
    })
  )
}
</script>

<style scoped lang="scss">
.area-props {
  overflow: scroll;
}

* {
  scrollbar-width: thin;
  scrollbar-color: #491988 #300748;
}
::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar:horizontal {
  height: 5px;
}
::-webkit-scrollbar-track {
  background: #300748;
  border-radius: 10px;
}
::-webkit-scrollbar-thumb {
  background: #491988;
  border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
  background: #5c26a2;
}
</style>