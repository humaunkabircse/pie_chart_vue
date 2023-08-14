<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const newItem = ref(16)
let chart = null

const dataset = [ 200, 150, 100 ]

const data = {
  labels: ['Red','Green','Blue'],
  datasets: [{
    label: 'My Task',
    data: dataset,
    backgroundColor: [
      'rgb(226, 0, 0)',
      'rgb(0, 155, 28)',
      'rgb(1, 122, 255)',
      'rgb(43, 105, 86)',
      'rgb(21, 21, 186)',
    ],
    hoverOffset: 4
  }]
};

const config = {
  type: 'pie',
  data: data,
};

onMounted(() => {
  const ctx = document.getElementById('chart')
  chart = new Chart(ctx, config)
})

function updateChart() {
  dataset.push(newItem.value)
  chart.data.datasets[0].data = dataset
  chart.update()
}

onBeforeUnmount(() => {
  chart.destroy()
})


</script>

<template>
  <div class=" mx-auto w-[400px] h-[400px] bg-gray-400">
    <canvas id="chart">
    </canvas>
  </div>

  <div class="mt-20">
    <input type="text" v-model="newItem">
    <button @click="updateChart()" class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Add
    </button>

  </div>
</template>

<style scoped></style>