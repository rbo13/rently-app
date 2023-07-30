<script setup lang="ts">
import data from "../data/data.json"

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

const apartments = ref([] as Apartments)

onMounted(() => {
  apartments.value = data?.apartments
})
</script>

<template>
  <div>
    <ApartmentList :apartments="apartments" />
  </div>
</template>

<style scoped></style>