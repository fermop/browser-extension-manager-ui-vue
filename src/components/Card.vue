<script setup>
  import Switch from './Switch.vue';

  const props = defineProps({
    card: {
      type: Object,
      required: true
    }
  })

  defineEmits(['remove-card'])
</script>

<template>
  <div
    class="h-[12.5rem] bg-neutral-0 dark:bg-neutral-800 p-4 rounded-[1.25rem] border-1 border-neutral-300 dark:border-neutral-600 shadow-xs flex flex-col justify-between"
  >
    <div
      class="flex gap-[1.25rem] items-start mb-[1.5rem]"
    >
      <img 
        :src="card.logo"
        :alt="card.name + ' logo'"
      >

      <div>
        <h2 class="text-xl text-neutral-900 dark:text-neutral-0 font-bold mb-1">{{ card.name }}</h2>
        <p class="text-base text-neutral-500 dark:text-neutral-400">{{ card.description }}</p>
      </div>
    </div>

    <div class="flex justify-between">
      <button
        class="text-neutral-900 dark:text-neutral-100 font-medium px-4 py-1 rounded-full border-1 border-neutral-300 dark:border-neutral-600 cursor-pointer hover:bg-red-500 hover:text-neutral-0 dark:hover:text-neutral-900 duration-250 focus:outline-offset-2 focus:outline-red-500"
        @click="$emit('remove-card', card)"
      >
        Remove
      </button>

      <Switch
        :card="card"
      />
    </div>
  </div>
</template>