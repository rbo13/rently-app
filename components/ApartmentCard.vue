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

const { apartment } = defineProps<{apartment: Apartment}>()

</script>

<template>
    <div class="bg-white shadow-md rounded-lg p-4 flex items-start space-x-4">
    <!-- <div class="mr-4">
      <img :src="apartment.photoUrl" alt="Apartment Image" class="w-24 h-24 rounded-lg object-cover">
    </div> -->

    <!-- Text in the center -->
    <div class="flex-1">
      <h2 class="text-xl font-semibold">
        Address: {{ apartment?.address.toUpperCase() }}
      </h2>
      <p class="text-gray-600">
        Floor: {{ apartment?.floor }}, Door #: {{ apartment?.doorNumber }}
      </p>
    </div>

    <!-- <div class="flex justify-center items-center">
      <div class="flex space-x-2">
        <NuxtLink :to="`/apartments/view/${apartment?.id}`" class="px-4 py-2 bg-blue-500 text-white rounded">
          View
        </NuxtLink>
        <NuxtLink :to="`/apartments/edit/${apartment?.id}`" class="px-4 py-2 bg-green-500 text-white rounded">
          Edit
        </NuxtLink>
      </div>
    </div> -->
  </div>
</template>

<style scoped></style>