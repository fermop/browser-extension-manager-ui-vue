<script setup>
  import { Switch } from '@headlessui/vue'

  const props = defineProps({
    card: {
      type: Object,
      required: true
    }
  })
</script>

<template>
  <Switch
    aria-label="toggler extention state"
    v-model="card.isActive"
    :class="card.isActive ? 'bg-red-500' : 'bg-neutral-300 dark:bg-neutral-600'"
    class="relative inline-flex h-6 w-11 items-center rounded-full cursor-pointer"
  >
    <span
      :class="card.isActive ? 'translate-x-6' : 'translate-x-1'"
      class="inline-block h-4 w-4 transform rounded-full bg-white transition"
    />
  </Switch>
</template>