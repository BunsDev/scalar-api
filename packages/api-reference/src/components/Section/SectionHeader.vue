<script setup lang="ts">
import LoadingSkeleton from '../LoadingSkeleton.vue'

withDefaults(
  defineProps<{ loading?: boolean; tight?: boolean; level?: number }>(),
  {
    loading: false,
    tight: false,
    level: 1,
  },
)
</script>

<template>
  <div class="section-header-wrapper">
    <LoadingSkeleton v-if="loading" />
    <component
      :is="`h${level}`"
      v-else
      class="section-header"
      :class="{ tight }">
      <slot />
    </component>
  </div>
</template>

<style scoped>
.section-header-wrapper {
  display: grid;
  grid-template-columns: 1fr;
}

@screen xl {
  .section-header-wrapper {
    grid-template-columns: repeat(2, 1fr);
  }
}

.section-header {
  font-size: var(--font-size, var(--scalar-heading-2));
  font-weight: var(--font-weight, var(--scalar-bold));
  /* prettier-ignore */
  color: var(--scalar-color-1);
  word-wrap: break-word;
  line-height: 1.45;
  margin-top: 0;
  margin-bottom: 12px;
}

.section-header.tight {
  margin-bottom: 6px;
}

.section-header.loading {
  width: 80%;
}
</style>
