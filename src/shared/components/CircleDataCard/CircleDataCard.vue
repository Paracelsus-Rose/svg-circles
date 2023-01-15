<script setup lang="ts">
import { useVModel } from '@vueuse/core'
import { CircleRenderVals } from 'types/Circle/RenderVals'

interface Props {
  circleRenderVals: CircleRenderVals
  title: string
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (event: 'update:circleRenderVals', payload: CircleRenderVals): void
}>()

const circleRenderVals = useVModel(props, 'circleRenderVals', emit)
</script>

<template>
  <div class="text-h6 row justify-center">
    {{ props.title }}
  </div>
  <div class="column justify-center row">
    <div
      class="inner-card-style-rr q-ma-sm"
      style="min-width: 170px"
    >
      <div class="text-h6 row justify-center">
        Target
      </div>
      <div class="q-px-md q-pb-md">
        <pre>{{ circleRenderVals.target }}</pre>
      </div>
    </div>
    <div
      class="inner-card-style-rr q-ma-sm"
      style="min-width: 170px"
    >
      <div class="text-h6 row justify-center">
        Destination
      </div>
      <div class="q-px-md q-pb-md">
        <pre>{{ circleRenderVals.destination }}</pre>
      </div>
    </div>
  </div>
</template>
