<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import data from "../../data/data.json"

export type Inventory = {
  id: number
  name: string
  quantity: string,
  imageUrl?: string,
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

const apartment = ref({} as Apartment)
const apartmentInventories = ref([] as Inventories)
const inventoriesOption = ref([] as Inventories)
const showForm = ref(false);

// Form fields
const newInventory = ref({
  name: '',
  quantity: '0'
})

const route = useRoute()
const id = route.params.id[0]

onMounted(() => {
  inventoriesOption.value = data.inventories

  if (id) {
    apartment.value = data.apartments.find((apartment) => apartment?.id === parseInt(id, 10))
    apartmentInventories.value = apartment?.value?.inventories
  }
})

const addNewInventory = () => {
  const upcomingInventory = {
    id: apartmentInventories?.value.length + 1,
    name: newInventory?.value?.name,
    quantity: newInventory?.value?.quantity
  } as Inventory;

  // if an inventory has added
  // just update the quantity.
  const foundInventory = apartmentInventories.value.filter((inventory) => inventory?.name === upcomingInventory?.name)
  if (foundInventory?.length > 0) {
    foundInventory[0].quantity = (parseInt(foundInventory[0].quantity, 10) + parseInt(upcomingInventory?.quantity, 10)).toString()
    closeInventoryForm()
    return
  }
  
  apartmentInventories.value.unshift(upcomingInventory)
  closeInventoryForm()
}


const cancelNewInventory = () => {
  closeInventoryForm()
}

const closeInventoryForm = () => {
  showForm.value = false;

  newInventory.value = {
    name: '',
    quantity: ''
  };
}

</script>

<template>
  <div class="max-w-lg mx-auto p-4">
    <div class="relative rounded-lg overflow-hidden">
      <div class="p-4 bg-white mt-4">
        <h2 class="text-xl font-bold mb-2">
          Address: {{ apartment?.address }}
        </h2>
        <p class="text-gray-600 mb-4">
          Floor: {{ apartment?.floor }}
        </p>
        <p class="text-gray-600">
          Door Number: {{ apartment?.doorNumber }}
        </p>
        <hr class="my-4 border-t border-gray-300">
        <div class="flex items-center justify-between mb-4">
          <h3 class="text-lg font-semibold mb-2">
          Inventories:
          </h3>
          <button @click="showForm = true">Add inventory</button>
        </div>
        <div v-if="showForm" div class="p-4 border border-gray-300 rounded-lg shadow-md mt-4 mb-4">
          <!-- Form to create a new inventory -->
          <form @submit.prevent="addNewInventory">
            <div class="mb-4">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="newItem">Select Inventory:</label>
              <select id="newItem" v-model="newInventory.name" class="mt-2 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
                <option value="" disabled selected>Select an item...</option>
                <option v-for="option in inventoriesOption" :key="option?.id" :value="option?.name">{{ option?.name }}</option>
              </select>
            </div>
            <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="newQuantity">New Quantity:</label>
            <input
              id="newQuantity"
              v-model.number="newInventory.quantity"
              type="number"
              min="1"
              class="form-input shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
          </div>

            <!-- Buttons to submit or cancel the form -->
            <div class="flex justify-end mt-4 space-x-2">
              <button type="submit" class="btn btn-primary">Create</button>
              <button type="button" @click="cancelNewInventory" class="btn btn-secondary">Cancel</button>
            </div>
          </form>
        </div>
        <InventoryList :inventories="apartmentInventories" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>