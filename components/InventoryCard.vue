<script setup lang="ts">
export type Inventory = {
  id: number
  name: string
  quantity: string,
  imageUrl?: string
}

export type Inventories = Inventory[]

export type Apartment = {
  id: number
  address: string
  floor: string
  doorNumber: string
  inventories: Inventories
}

export type Apartments = Apartment[]

const props = defineProps<{inventory: Inventory}>()
</script>

<template>
  <div class="p-4 border border-gray-300 rounded-lg shadow-md">
    <h2 class="text-lg font-semibold mb-2">
      {{ props.inventory?.name }}
    </h2>
    <p class="text-gray-600 mb-4">
      Quantity: {{ props.inventory?.quantity }}
    </p>
  </div>
</template>

<style scoped></style>