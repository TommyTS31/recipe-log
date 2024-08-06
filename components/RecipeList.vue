<template>
  <div class="mt-4 flex justify-center">
    <div class="flex flex-col">
      <div v-for="meal in data">
        <RecipeCard :meal_name="meal.meal_name" :image_link="meal.image_link" />
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const { data, error } = await client.from("recipe-list").select();
console.log(data);
</script>
