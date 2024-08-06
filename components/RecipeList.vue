<template>
  <div class="mt-4 flex justify-center">
    <div class="flex flex-col">
      <div v-for="meal in data">
        <RecipeCard
          :meal_name="meal.meal_name"
          :image_link="meal.image_link"
          :carbs="meal.carbs"
          :protein="meal.protein"
          :extra="meal.extra"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const { data, error } = await client.from("recipe-list").select();
</script>
