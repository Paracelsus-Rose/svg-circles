<script setup lang="ts">
import { useVModel } from '@vueuse/core'
import { Dimensions } from 'types/Circle/Dimensions'

interface Props {
  strokeWidth: number
  widthMultiplier: number
  heightMultiplier: number
  dimensions: Dimensions

}

const props = defineProps<Props>()

const emit = defineEmits<{
  (event: 'update:strokeWidth', payload: number): void
  (event: 'update:widthMultiplier', payload: number): void
  (event: 'update:heightMultiplier', payload: number): void
  (event: 'update:dimensions', payload: Dimensions): void

}>()

const strokeWidth = useVModel(props, 'strokeWidth', emit)
const widthMultiplier = useVModel(props, 'widthMultiplier', emit)
const heightMultiplier = useVModel(props, 'heightMultiplier', emit)
const dimensions = useVModel(props, 'dimensions', emit)

</script>

<template>
  <q-card
    class="card-style-rr q-ma-sm"
    style="min-width: 200px; min-height: 300px;"
  >
    <div class="text-h6 q-pa-md row justify-center">
      Circle Config
    </div>
    <div class="q-px-md q-pb-md">
      Stroke Width: {{ strokeWidth }}
      <q-slider
        v-model="strokeWidth"
        color="green"
        :min="2"
        :step="1"
        :max="15"
      />
    </div>
    <div class="q-px-md q-pb-md">
      Width Mult: {{ widthMultiplier }}
      <q-slider
        v-model="widthMultiplier"
        color="green"
        :min="4"
        :step="1"
        :max="20"
      />
    </div>
    <div class="q-px-md q-pb-md">
      Heigh Mult: {{ heightMultiplier }}
      <q-slider
        v-model="heightMultiplier"
        color="green"
        :min="4"
        :step="1"
        :max="20"
      />
    </div>
    <div class="text-h6 q-pa-md row justify-center">
      Arrowhead <br>Dimensions:
    </div>
    <div class="q-mx-md q-mb-md">
      Width: {{ dimensions.width }} <br>
      Height: {{ dimensions.height }}
    </div>
  </q-card>
</template>
