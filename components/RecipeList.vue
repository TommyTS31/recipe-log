<template>
  <div class="flex flex-col w-full px-1 sm:w-3/5 md:w-2/3">
    <div class="flex mt-4">
      <div class="grow">
        <input
          type="text"
          placeholder="Search"
          class="text-md font-sans w-full py-1.5 px-2 border border-gray-300 rounded-md"
        />
      </div>
      <button
        class="bg-black hover:bg-blackbg px-6 py-1.5 mx-2 w-1/5 rounded-md shadow-sm text-white"
        @click="displayFilter ? (displayFilter = false) : (displayFilter = true)"
      >
        Filter
      </button>
      <DisplayPicker
        @displayOption="setDisplayChoice"
        v-if="!isMobile"
        :displayChoice="displayChoice"
      />
    </div>
    <Filter v-if="displayFilter" />
    <div
      class="mt-4 grid grid-cols-1 justify-center justify-items-center"
      v-if="displayChoice"
    >
      <div v-for="meal in data" class="lg:w-2/3 md:w-full sm:w-full w-full">
        <RecipeCard
          :meal_name="meal.meal_name"
          :image_link="meal.image_link"
          :carbs="meal.carbs"
          :protein="meal.protein"
          :extra="meal.extra"
          :id="meal.id"
          :displayOption="displayChoice"
        />
      </div>
    </div>
    <div class="grid grid-cols-3 mt-1" v-else>
      <div v-for="meal in data">
        <RecipeCard
          :meal_name="meal.meal_name"
          :image_link="meal.image_link"
          :carbs="meal.carbs"
          :protein="meal.protein"
          :extra="meal.extra"
          :id="meal.id"
          :displayOption="displayChoice"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
const option = ref(false);
const displayFilter = ref(false);
const displayChoice = ref(true);
const client = useSupabaseClient();
const { data, error } = await client.from("recipe-list").select();

const isMobile = computed(() => {
  const { width } = useWindowSize();
  if (width.value >= 1350) {
    return false;
  } else {
    displayChoice.value = true;
    return true;
  }
});

function setDisplayChoice(n) {
  displayChoice.value = n;
  console.log(displayChoice.value);
}
</script>
