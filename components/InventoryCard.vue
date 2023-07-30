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
  inventory: Inventory
}>()

const updateInventory = ref({
  name: props.inventory.name,
  quantity: props.inventory.quantity
})

const showForm = ref(false)

const cancelNewInventory = () => {
  showForm.value = false
}

const handleUpdateInventory = () => {
  props.inventory.name = updateInventory.value.name
  props.inventory.quantity = updateInventory.value.quantity
  showForm.value = false
}

</script>

<template>
  <div class="p-4 border border-gray-300 rounded-lg shadow-md">
    <div v-if="!showForm">
      <h2 class="text-lg font-semibold mb-2">
        {{ props.inventory?.name }}
      </h2>
      <p class="text-gray-600 mb-4">
        Quantity: {{ props.inventory?.quantity }}
      </p>
      <button class="btn bg-blue-500 text-white" @click="showForm = true">
        Update Inventory
      </button>
    </div>

    <div v-if="showForm" class="mt-4">
      <div class="space-y-2">
        <form @submit.prevent="handleUpdateInventory">
          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="newItem">New Item Name:</label>
            <input
              id="newItem"
              v-model="updateInventory.name"
              class="form-input shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              type="text"
              placeholder="New Item Name"
            >
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="newQuantity">New Quantity:</label>
            <input
              id="newQuantity"
              v-model.number="updateInventory.quantity"
              type="number"
              min="1"
              class="form-input shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            >
          </div>

          <div class="flex justify-end mt-4 space-x-2">
            <button type="submit" class="btn btn-update-inventory">
              Save
            </button>
            <button type="button" @click="cancelNewInventory" class="btn btn-secondary">
              Cancel
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Custom style for the "Update Inventory" button */
.btn-update-inventory {
  background-color: #3b82f6;
  color: #fff;
}

/* Remove the hover effect on the "Update Inventory" button */
.btn:hover {
  background-color: #3b82f6;
}

</style>