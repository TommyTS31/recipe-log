<template>
  <div class="border border-gray-300 bg-white rounded-md mt-4">
    <div class="px-6 py-3">
      <p class="text-gray-500 text-sm">Filter</p>
      <div>
        <label class="block mb-2 text-sm font-medium mt-2">Carbs</label>
        <ul class="flex flex-row flex-wrap justify-center w-full">
          <li v-for="carb in carbsChoices" class="flex m-0.5 grow w-1/4 flex-wrap">
            <input
              type="checkbox"
              name="Carbs"
              :id="carb"
              class="py-2 mx-1.5 w-5 hidden peer"
              :value="carb"
            />
            <label
              class="block text-sm font-sans font-medium px-2 mb-0.5 w-full h-full py-1.5 text-gray-500 bg-white border border-gray-200 rounded-md cursor-pointer peer-checked:border-blackbg peer-checked:text-blackbg hover:text-gray-600 hover:bg-gray-100"
              :for="carb"
              >{{ carb }}</label
            >
          </li>
        </ul>
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium mt-2">Protein</label>
        <ul class="flex flex-row flex-wrap justify-center w-full">
          <li v-for="protein in proteinChoices" class="flex m-0.5 grow w-1/4 flex-wrap">
            <input
              type="checkbox"
              name="Proteins"
              :id="protein"
              :value="protein"
              class="py-2 mx-1.5 w-5 hidden peer"
            />
            <label
              class="block text-sm font-sans font-medium px-2 mb-0.5 w-full h-full py-1.5 text-gray-500 bg-white border border-gray-200 rounded-md cursor-pointer peer-checked:border-blackbg peer-checked:text-blackbg hover:text-gray-600 hover:bg-gray-100"
              :for="protein"
              >{{ protein }}</label
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
const proteinChoices = ref([
  "Chicken (Thigh)",
  "Chicken (Breast)",
  "Chicken (Wings)",
  "Beef (Ground)",
  "Steak",
  "Pork (Lean / Shoulder)",
  "Pork (Ground)",
  "Shrimp",
  "Eggs",
  "Pork (Belly)",
  "Salmon",
  "N/A",
]);
const carbsChoices = ref(["Rice", "Rice Cake", "Noodles"]);
</script>
