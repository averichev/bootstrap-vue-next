<template>
  <b-container>
    <button ref="reference">Button</button> {{ x }} {{ y }}, {{ middlewareData }}
    <div
      ref="floating"
      :style="{
        position: strategy,
        top: `${y ?? 0}px`,
        left: `${x ?? 0}px`,
        width: 'max-content',
      }"
    >
      <div
        id="arrow"
        ref="arroww"
        style="w-4 h-4 bg-gray-800 [left:-0.5rem]; width: 10px ; height:10px; background-color: red"
      />
      Tooltipswowoowowow
    </div>
  </b-container>
</template>

<script setup lang="ts">
import {computed, ref, toRef, useSlots, watch} from 'vue'
import {arrow, useFloating} from '@floating-ui/vue'
// You can use this file as a development spot to test your changes
// Please do not commit this file

// errors on initial page load
const arroww = ref(null)

const reference = ref(null)
const floating = ref(null)
const {x, y, strategy, middlewareData} = useFloating(reference, floating, {
  middleware: [arrow({element: arroww})],
})

console.log(middlewareData)
</script>
