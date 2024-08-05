<template>
  <div class="flex justify-center mt-5">
    <div
      class="shadow w-11/12 md:w-3/4 lg:w-7/12 bg-gray-50 font-sans font-medium p-4 rounded-md"
    >
      <div>
        <label class="block mb-2 text-sm font-medium">Meal Name</label>
        <input
          type="text"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 mb-2"
          placeholder="Chicken and rice"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium">Description</label>
        <textarea
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 mb-2"
          placeholder="Chicken and rice"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium">Carbs</label>
        <input
          type="text"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 mb-2"
          placeholder="Rice"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium">Protein</label>
        <ul class="flex flex-row flex-wrap justify-center">
          <li v-for="protein in proteinChoices" class="flex w-1/4 m-0.5">
            <input
              type="radio"
              name="Proteins"
              :id="protein"
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
  "Pork (Lean/Shoulder)",
  "Pork (Ground)",
  "Shrimp",
  "Eggs",
]);
</script>
