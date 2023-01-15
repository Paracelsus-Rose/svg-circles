<script setup lang="ts">
import { useVModel } from '@vueuse/core'
import { CircleAdjustments } from 'types/Circle/CircleAdjustments'

interface Props {
  circleAdjustments: CircleAdjustments
  visible: boolean
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (event: 'update:circleAdjustments', payload: CircleAdjustments): void
  (event: 'update:visible', payload: boolean): void
}>()

const circleAdjustments = useVModel(props, 'circleAdjustments', emit)
const visible = useVModel(props, 'visible', emit)

</script>

<template>
  <q-slide-transition>
    <div v-show="visible">
      <q-card
        class="card-style-rr"
        style="min-width: 100px; min-height: 100px;"
      >
        <div class="text-subtitle1 q-pa-md row justify-center">
          Circle Adjustments
        </div>
        <div class="q-px-md q-pb-md">
          Target cX Offset: {{ circleAdjustments.targetCxOffset }}
          <q-slider
            v-model="circleAdjustments.targetCxOffset"
            color="green"
            :min="0.1"
            :step="0.1"
            :max="5"
          />
        </div>
        <div class="q-px-md q-pb-md">
          Destination cX Offset: {{ circleAdjustments.destinationCxOffset }}
          <q-slider
            v-model="circleAdjustments.destinationCxOffset"
            color="green"
            :min="0.1"
            :step="0.1"
            :max="5"
          />
        </div>
        <div class="q-px-md q-pb-md">
          cY Offset: {{ circleAdjustments.cYOffset }}
          <q-slider
            v-model="circleAdjustments.cYOffset"
            color="green"
            :min="0.1"
            :step="0.05"
            :max="4"
          />
        </div>
        <div class="q-px-md q-pb-md">
          Radius Offset: {{ circleAdjustments.radiusOffset }}
          <q-slider
            v-model="circleAdjustments.radiusOffset"
            color="green"
            :min="0.1"
            :step="0.05"
            :max="4"
          />
        </div>
      </q-card>
    </div>
  </q-slide-transition>
</template>
