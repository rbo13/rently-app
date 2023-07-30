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

const props = defineProps<{
  inventories: Inventories
  preview: boolean
}>()

</script>

<template>
  <div class="space-y-4">
    <InventoryCard v-for="inventory in props.inventories" :key="inventory?.id" :inventory="inventory" :preview="preview" />
  </div>
</template>

<style scoped></style>