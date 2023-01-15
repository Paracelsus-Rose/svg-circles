<script setup lang="ts">
import { ref } from 'vue'
import { useVModel } from '@vueuse/core'
import { CircleRenderVals } from 'types/Circle/RenderVals'

interface Props {
  renderVals: CircleRenderVals
  strokeWidth: number
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (event: 'update:renderVals', payload: CircleRenderVals): void
  (event: 'update:strokeWidth', payload: number): void
}>()

const renderVals = useVModel(props, 'renderVals', emit)
const strokeWidth = useVModel(props, 'strokeWidth', emit)
const viewBoxSize = ref(30)

</script>

<template>
  <svg
    style="border-radius: 12px"
    class="q-ma-sm"
    :viewBox="`0 0 ${viewBoxSize} ${viewBoxSize}`"
  >
    <rect
      x="0"
      y="0"
      :width="viewBoxSize"
      :height="viewBoxSize"
      fill="grey"
    />
    <circle
      :cx="renderVals.target.cx"
      :cy="renderVals.target.cy"
      :r="renderVals.target.r"
      :style="`fill: red; stroke: darkred; stroke-width: ${strokeWidth}px;`"
    />
    <text
      :x="renderVals.target.cx"
      :y="renderVals.target.cy - renderVals.target.r - 3"
      style="font-size: 2px; text-anchor: middle; dominant-baseline: hanging;"
    >
      Target
    </text>

    <text
      x="50%"
      y="90%"
      style="font-size: 2px; text-anchor: middle; dominant-baseline: middle;"
    >
      Diameter: {{ renderVals.target.r * 2 }}
    </text>
    <circle
      :cx="renderVals.target.cx"
      :cy="renderVals.target.cy"
      :r="renderVals.target.r / 16"
      :style="`fill: darkred; stroke: none;`"
    />
    <circle
      :cx="renderVals.destination.cx"
      :cy="renderVals.destination.cy"
      :r="renderVals.destination.r"
      :style="`fill: green; stroke: darkgreen; stroke-width: ${strokeWidth}px; opacity: 0.7;`"
    />

    <text
      :x="renderVals.destination.cx"
      :y="renderVals.destination.cy - renderVals.destination.r - 3"
      style="font-size: 2px; text-anchor: middle; dominant-baseline: hanging;"
    >
      Destination
    </text>
    <text
      :x="renderVals.destination.cx / 1.3"
      :y="renderVals.destination.cy"
      :dy="-3"
      style="font-size: 1px; text-anchor: start;"
    >
      Destination({{ renderVals.destination.cx }}, {{ renderVals.destination.cy }})
    </text>
    <circle
      :cx="renderVals.destination.cx"
      :cy="renderVals.destination.cy"
      :r="renderVals.destination.r / 16"
      :style="`fill: darkgreen; stroke: none;`"
    />
    <circle
      :cx="viewBoxSize / 2"
      :cy="viewBoxSize / 2"
      r="0.5"
      style="fill: blue;"
    />
    <text
      :x="viewBoxSize / 2.5"
      :y="viewBoxSize / 2"
      :dy="-1"
      style="font-size: 1px; text-anchor: start;"
    >
      Center ({{ viewBoxSize / 2 }}, {{ viewBoxSize / 2 }})
    </text>
    <text
      :x="renderVals.target.cx / 1.2"
      :y="renderVals.target.cy"
      :dy="-2"
      style="font-size: 1px; text-anchor: start;"
    >
      Target({{ renderVals.target.cx }}, {{ renderVals.target.cy }})
    </text>
  </svg>
</template>
