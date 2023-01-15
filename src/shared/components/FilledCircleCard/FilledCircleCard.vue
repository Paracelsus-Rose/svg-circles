<script setup lang="ts">
import { useVModel } from '@vueuse/core'
import { CircleAdjustments } from 'types/Circle/CircleAdjustments'
import { Dimensions } from 'types/Circle/Dimensions'
import { CircleRenderVals } from 'types/Circle/RenderVals'
import { computed, ref } from 'vue'
import CircleDataCard from '../CircleDataCard/CircleDataCard.vue'
import CircleSvgRender from '../CircleSVGRender/CircleSvgRender.vue'
import ExpandCircleAdjustmentCard from '../ExpandCircleAdjustmentCard/ExpandCircleAdjustmentCard.vue'

interface Props {
  dimensions: Dimensions
  strokeWidth: number
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (event: 'update:dimensions', payload: Dimensions): void
  (event: 'update:strokeWidth', payload: number): void
}>()

const dimensions = useVModel(props, 'dimensions', emit)
const strokeWidth = useVModel(props, 'strokeWidth', emit)

const circleAdjustments = ref<CircleAdjustments>({
  targetCxOffset: 10,
  destinationCxOffset: 10,
  cYOffset: 1.6,
  radiusOffset: 3.2,
})

const filledCircleVals = computed(() => {
  const calcCyR = {
    cy: parseFloat(((dimensions.value.height / circleAdjustments.value.cYOffset) / strokeWidth.value * 2).toFixed(2)),
    r: parseFloat(((dimensions.value.width / circleAdjustments.value.radiusOffset) / strokeWidth.value * 2).toFixed(2)),
  }

  const target = {
    cx: parseFloat(((dimensions.value.height / circleAdjustments.value.cYOffset) / strokeWidth.value * 2).toFixed(2)),
    ...calcCyR,
  }

  const destination = {
    cx: parseFloat(((dimensions.value.height / circleAdjustments.value.cYOffset) / strokeWidth.value * 2).toFixed(2)),
    ...calcCyR,
  }

  const renderVals: CircleRenderVals = {
    target,
    destination,
  }

  return { renderVals }
})

const visible = ref(false)

const title = ref('Target')
</script>

<template>
  <div class="column">
    <q-card
      class="card-style-rr q-ma-sm q-pa-sm column justify-center"
      style="min-width: 200px; min-height: 150px;"
    >
      <CircleDataCard
        v-model:circle-render-vals="filledCircleVals.renderVals"
        title="Filled Circle"
      />
      <ExpandCircleAdjustmentCard
        v-model:circle-adjustments="circleAdjustments"
        v-model:visible="visible"
      />
    </q-card>
    <CircleSvgRender
      v-model:render-vals="filledCircleVals.renderVals"
      v-model:stroke-width="strokeWidth"
      :title="title"
    />
  </div>
</template>
