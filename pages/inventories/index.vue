<script setup lang="ts">
import { ref, onMounted } from 'vue'
import data from "../../data/data.json"

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

const showForm = ref(false)
const showPreview = ref(false)
const showModal = ref(false)
const tempInventories = ref([] as Inventories)

const formFields = ref({
  name: '',
  quantity: '0'
})

onMounted(() => {
})

const addPreviewInventory = () => {
  if (!formFields.value.name) {
    return;
  }

  tempInventories.value.unshift({
    id: 0,
    name: formFields?.value?.name,
    quantity: formFields?.value?.quantity,
    imageUrl: ""
  })

  // clear value
  formFields.value.name = ''
  formFields.value.quantity = '0'
  showPreview.value = true
}

const closeModal = () => {
  showModal.value = false
}

</script>

<template>
  <div>
    <div class="px-4 py-4">
      <div class="flex items-center justify-between mb-4">
        <button @click="showForm = true" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Add inventory</button>
      </div>

      <div v-if="showForm">
        <div class="w-full max-w-xs">
          <form @submit.prevent="addPreviewInventory" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <div class="mb-4">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="inventoryName">
                Inventory Name
              </label>
              <input 
                id="inventoryName"
                v-model="formFields.name"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                type="text"
                placeholder="Name" />
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="newQuantity">Quantity:</label>
              <input
                id="newQuantity"
                v-model.number="formFields.quantity"
                type="number"
                min="1"
                class="form-input w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              >
            </div>
            <div class="flex items-center justify-between">
              <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                Add
              </button>
            </div>
          </form>
        </div>
      </div>

      <div v-if="showPreview">
        <button @click="showModal = true" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded">Show Preview</button>
      </div>
    </div>

    <AppModal :showModal="showModal" :onClose="closeModal" :inventoryList="tempInventories" />
  </div>  
</template>

<style scoped></style>