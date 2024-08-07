<template>
  <div class="flex justify-center mt-16">
    <div class="w-11/12 lg:w-1/2 font-sans rounded-md">
      <div class="lg:flex lg:justify-between">
        <p class="font-sans text-3xl font-medium mb-3 lg:mb-0">{{ meal.meal_name }}</p>
        <a
          class="bg-white hover:bg-gray-50 border border-gray-300 text-black text-md px-3 py-1 rounded-md shadow-sm h-min"
          href="/"
          >Edit Meal</a
        >
      </div>
      <hr class="h-px my-4 bg-gray-200 border-0" />
      <div class="lg:flex lg:space-x-3 bg-white rounded p-4 border border-gray-300">
        <NuxtImg
          class="w-full h-80 object-cover rounded-md border-2 border-gray-300"
          :src="img(responseImage.data.publicUrl)"
        />
        <div class="flex flex-col justify-between">
          <div class="mt-3 lg:mt-0">
            <p class="text-sm text-gray-500">Description</p>
            <p class="text-md font-regular text-justify leading-5">
              {{ meal.description }}
            </p>
            <hr class="h-px my-4 bg-gray-200 border-0" />
            <div class="flex space-x-8">
              <div>
                <p class="text-sm text-gray-500">Carbs</p>
                <p class="text-md font-regular text-justify leading-5">
                  {{ meal.carbs }}
                </p>
              </div>
              <div>
                <p class="text-sm text-gray-500">Protein</p>
                <p class="text-md font-regular text-justify leading-5">
                  {{ meal.protein }}
                </p>
              </div>
              <div>
                <p class="text-sm text-gray-500">Extra</p>
                <p class="text-md font-regular text-justify leading-5">
                  {{ meal.extra }}
                </p>
              </div>
            </div>
          </div>
          <div class="mt-6 lg:mt-0">
            <p class="text-sm text-gray-500">Date Added</p>
            <p class="text-md font-regular text-justify leading-5">
              {{ parseDate(meal.created_at) }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const img = useImage();
const id = useRoute().params.id;

function newPath(path) {
  const segments = path.split("/");
  segments.shift();
  const newPath = segments.join("/");
  return newPath;
}

const { data, error } = await client.from("recipe-list").select().eq("id", id);
const meal = data[0];

const responseImage = await client.storage
  .from("Meal Images")
  .getPublicUrl(newPath(meal.image_link));

function parseDate(date) {
  const dateObject = new Date(date);
  const dateString = dateObject.toDateString();
  return dateString;
}
</script>
