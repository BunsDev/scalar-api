<script setup lang="ts">
import { ref } from 'vue'

import { ScalarIconButton } from '../ScalarIconButton'
import { ICONS } from './icons'

defineProps<{
  thickness?: string
}>()

defineOptions({ inheritAttrs: false })

const copyToClipboard = (value: string) =>
  navigator.clipboard.writeText(value).then(() => {
    copied.value = true
    setTimeout(() => (copied.value = false), 1500)
  })

const selected = ref('')
const copied = ref(false)
</script>
<template>
  <div class="flex flex-col divide-y rounded border bg-b-1">
    <div class="flex flex-wrap gap-2 p-0.5">
      <ScalarIconButton
        v-for="icon in ICONS"
        :key="icon"
        class="hover:bg-b-2"
        :icon="icon"
        :label="icon"
        :thickness="thickness"
        v-bind="$attrs"
        @click="copyToClipboard(icon)"
        @mouseenter="selected = icon" />
    </div>
    <div class="flex justify-between p-2 text-xs text-c-2">
      <span v-if="copied">Copied to clipboard!</span>
      <span v-else>Select an icon to copy</span>
      <code class="font-code">
        {{ selected }}
      </code>
    </div>
  </div>
</template>
