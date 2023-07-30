<script setup lang="ts">
import { ref } from 'vue'

const searchTerm = ref('')

const handleSearch = () => {
  const { value } = searchTerm
  console.log('Searching...', value)
}
</script>

<template>
  <header class="bg-blue-500 py-4 px-8">
    <div class="flex items-center justify-between">
      <h1 class="text-black text-2xl font-bold">
        <NuxtLink to="/">
          Rently
        </NuxtLink>
      </h1>
      <div class="flex items-center">
        <input
          v-model="searchTerm"
          class="border border-gray-300 rounded px-4 py-2 mr-2"
          placeholder="Search for apartments..."
          @input="handleSearch"
        >
        <button class="bg-white text-blue-500 px-4 py-2 rounded" @click="handleSearch">
          Search
        </button>
      </div>
      <nav class="space-x-4">
        <!-- <NuxtLink to="/" class="text-black hover:underline">
          Apartments
        </NuxtLink>
        <NuxtLink to="/inventories" class="text-black hover:underline">
          Inventory
        </NuxtLink> -->
      </nav>
    </div>
  </header>
</template>

<style scoped>

.router-link-exact-active {
  text-decoration: underline;
}

</style>
