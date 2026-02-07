<script setup>
  import { ref, reactive, onMounted, computed } from 'vue'

  import { db } from './data/data.js'

  import Header from './components/Header.vue'
  import Card from './components/Card.vue';
  import Footer from './components/Footer.vue'

  const state = reactive({
    darkMode: false
  })

  const cards = ref([])

  const filter = ref('all')

  const cardsFilter = computed(() => {
    if (filter.value === 'active') {
      return cards.value.filter(card => card.isActive)
    } else if (filter.value === 'inactive') {
      return cards.value.filter(card => !card.isActive)
    }
    return cards.value
  })

  const card = ref({})

  onMounted(() => {
    cards.value = db

    const isActive = localStorage.getItem('dark-mode') === 'true'

    if (isActive) {
      toggleDarkMode()
    }
  })

  const toggleDarkMode = () => {
    document.body.classList.toggle('dark')
    state.darkMode = !state.darkMode
    localStorage.setItem('dark-mode', state.darkMode)
  }

  const showAll = () => {filter.value = 'all'}
  const showActive = () => {filter.value = 'active'}
  const showInActive = () => {filter.value = 'inactive'}
  const removeCard = (card) => {
    return cards.value = cards.value.filter(cardInCards => cardInCards !== card)
  }

  
</script>

<template>
  <div class="w-[90%] max-w-[73.25rem] m-auto pt-8 min-h-[100vh]">
    <Header
      @toggle-dark-mode="toggleDarkMode"
      v-model:darkMode="state.darkMode"
    />

    <main 
      class="mt-8"
    >
      <header
        class="md:flex md:items-center md:justify-between md:mb-10"
      >
        <h1 
          class="text-neutral-900 dark:text-neutral-0 font-bold text-3xl text-center"
        >Extensions List</h1>

        <div
          class="flex w-fit mt-4 mb-8 m-auto gap-4 md:m-0"
        >
          <button 
            :class="[filter === 'all' ? 'border-red-400 bg-red-500 text-neutral-0 dark:text-neutral-900' : 'bg-neutral-0 dark:bg-neutral-700']"
            class="dark:text-neutral-0 py-[.25rem] text-lg px-4 border-1 rounded-full cursor-pointer hover:opacity-[.7] duration-250 border-neutral-300 focus:outline-red-500 focus:outline-offset-3"
            @click="showAll"
          >
            All
          </button>
          <button 
            :class="[filter === 'active' ? 'border-red-400 bg-red-500 text-neutral-0 dark:text-neutral-900' : 'bg-neutral-0 dark:bg-neutral-700']"
            class="dark:text-neutral-0 py-[.25rem] text-lg px-4 border-1 rounded-full cursor-pointer hover:opacity-[.7] duration-250 border-neutral-300 focus:outline-red-500 focus:outline-offset-3"
            @click="showActive"
          >
            Active
          </button>
          <button 
            :class="[filter === 'inactive' ? 'border-red-400 bg-red-500 text-neutral-0 dark:text-neutral-900' : 'bg-neutral-0 dark:bg-neutral-700']"
            class="dark:text-neutral-0 py-[.25rem] text-lg px-4 border-1 rounded-full cursor-pointer hover:opacity-[.7] duration-250 border-neutral-300 focus:outline-red-500 focus:outline-offset-3"
            @click="showInActive"
          >
            Inactive
          </button>
        </div>
      </header>

      <div 
        class="grid md:grid-cols-2 lg:grid-cols-3 gap-4"
      >
        <Card
          v-for="card in cardsFilter"
          :card="card"
          @remove-card="removeCard"
        />
      </div>
    </main>
  </div>

  <!-- <Footer/> -->
  <Footer
    class="text-center text-[.6875rem] my-8"
  />
</template>