<script setup lang="ts">
import CircleAdjustmentsCard from '../CircleAdjustmentsCard/CircleAdjustmentsCard.vue'
import { useVModel } from '@vueuse/core'
import { CircleAdjustments } from 'types/Circle/CircleAdjustments'
import { computed } from 'vue'

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

const icon = computed(() => {
  if (!visible.value) {
    return 'expand_more'
  } else {
    return 'expand_less'
  }
})
</script>

<template>
  <q-btn
    :icon="icon"
    style="margin:auto;"
    @click="visible = !visible"
  />
  <CircleAdjustmentsCard
    v-model:circle-adjustments="circleAdjustments"
    v-model:visible="visible"
  />
</template>
