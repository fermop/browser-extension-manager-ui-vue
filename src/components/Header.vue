<script setup>
  defineEmits(['toggle-dark-mode', 'update:state'])

  const props = defineProps({
    darkMode: {
      type: Boolean,
      required: true
    }
  })
</script>

<template>
  <header 
    class="w-full bg-neutral-0 dark:bg-neutral-800 p-[.5rem] flex justify-between shadow-sm rounded-md"
  >
    <img 
      src="/assets/images/logo.svg"
      alt="Logo"
    >

    <button 
      class="bg-neutral-100 dark:bg-neutral-700 hover:bg-neutral-300 dark:hover:bg-neutral-600 p-3 duration-250 cursor-pointer rounded-xl focus:outline-red-400"
      @click="$emit('toggle-dark-mode')"
    >
      <img 
        :src="[props.darkMode ? '/assets/images/icon-sun.svg' : '/assets/images/icon-moon.svg']" 
        alt="Toggle mode icon"
      >
    </button>
  </header>
</template>