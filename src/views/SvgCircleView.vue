<script setup lang="ts">
import CircleCard from 'src/shared/components/CircleCard/CircleCard.vue'
import CircleConfigCard from 'src/shared/components/CircleConfigCard/CircleConfigCard.vue'
import FilledCircleCard from 'src/shared/components/FilledCircleCard/FilledCircleCard.vue'
import { Dimensions } from 'types/Circle/Dimensions'
import { computed, ref } from 'vue'

const MIN_ARROWHEAD_STROKE_WIDTH = 2

const strokeWidth = ref(2)
const widthMultiplier = ref(12)
const heightMultiplier = ref(12)

const dimensions = computed(() => {
  const clippedStroke = Math.max(MIN_ARROWHEAD_STROKE_WIDTH, strokeWidth.value)

  const width = clippedStroke * widthMultiplier.value
  const height = clippedStroke * heightMultiplier.value

  const dimensions: Dimensions = {
    width,
    height,
  }
  return { dimensions }
})

</script>

<template>
  <q-page class="flex flex-center row">
    <CircleConfigCard
      v-model:stroke-width="strokeWidth"
      v-model:width-multiplier="widthMultiplier"
      v-model:height-multiplier="heightMultiplier"
      v-model:dimensions="dimensions.dimensions"
    />
    <div
      class=" row items-start justify-between"
      style="flex-wrap:nowrap;"
    >
      <FilledCircleCard
        v-model:dimensions="dimensions.dimensions"
        v-model:stroke-width="strokeWidth"
      />

      <CircleCard
        v-model:dimensions="dimensions.dimensions"
        v-model:stroke-width="strokeWidth"
      />
    </div>
  </q-page>
</template>
