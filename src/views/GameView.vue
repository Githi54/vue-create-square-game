<script setup>
import { ref, watch } from 'vue'

const sizeX = ref(5)
const sizeY = ref(10)

const grid = ref([])

watch([sizeX, sizeY], () => {
  createGrid()
})

function createGrid() {
  grid.value = Array.from({ length: sizeY.value }).fill(
    Array.from({ length: sizeX.value }).fill(false)
  )
}

createGrid()
</script>

<template class="template">
  <div class="container">
    <v-card class="size">
      <v-card-title>Size</v-card-title>
      <v-card-text>
        <v-text-field v-model="sizeX" label="Size X" type="number"></v-text-field>
        <v-text-field v-model="sizeY" label="Size Y" type="number"></v-text-field>
      </v-card-text>
    </v-card>
    <div>
      <div class="square-container">
        <div v-for="(row, rowIndex) in grid" :key="rowIndex" class="square-rows">
          <div v-for="(_, colIndex) in row" :key="colIndex" class="square"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.template {
  overflow-x: auto;
}

.container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.square-container {
  display: flex;
  flex-direction: column;

  width: max-content;
}

.square-rows {
  display: flex;

  width: max-content;
}

.size {
  width: 200px;
}

.square {
  width: 36px !important;
  height: 36px !important;
  margin: 1px;
  cursor: pointer;

  background-color: white;
}

.square:hover {
  background-color: blue;
}

.blue {
  background-color: blue;
}

.white {
  background-color: white;
}
</style>
