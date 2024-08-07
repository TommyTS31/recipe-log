<template>
  <div
    class="flex flex-col w-11/12 sm:w-3/5"
    v-bind:class="displayChoice ? 'md:w-3/4' : 'md:w-3/4'"
  >
    <div class="flex mt-4">
      <div class="grow">
        <input
          type="text"
          placeholder="Search"
          class="text-md font-sans w-full py-1.5 px-2 border border-gray-300 rounded-md"
        />
      </div>
      <DisplayPicker
        @displayOption="setDisplayChoice"
        v-if="!isMobile"
        :displayChoice="displayChoice"
      />
    </div>
    <div class="mt-4 flex grow" v-if="displayChoice">
      <div class="flex flex-col grow">
        <div v-for="meal in data">
          <RecipeCard
            :meal_name="meal.meal_name"
            :image_link="meal.image_link"
            :carbs="meal.carbs"
            :protein="meal.protein"
            :extra="meal.extra"
            :id="meal.id"
          />
        </div>
      </div>
      <div></div>
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
        />
      </div>
    </div>
  </div>
</template>

<script setup>
const option = ref(false);
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
}
</script>
