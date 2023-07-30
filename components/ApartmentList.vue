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

const props = defineProps<{ apartments: Apartments }>()
</script>

<template>
    <div class="flex flex-col items-center">
    <h2 class="text-2xl font-semibold mb-4">
      Apartment Listings
    </h2>
    <div class="grid grid-cols-1 gap-4">
      <ApartmentCard v-for="apartment in props.apartments" :key="apartment?.id" :apartment="apartment" />
    </div>
  </div>
</template>