<template>
  <div
    class="flex flex-col md:flex-row bg-whitealt shadow-sm hover:shadow-md duration-150 rounded-md border border-gray-200 my-1 mx-0.5 md:mx-1"
  >
    <div>
      <NuxtImg
        class="h-72 md:h-48 md:w-48 w-full object-cover rounded-l-md"
        :src="img(data.publicUrl)"
      />
    </div>
    <div class="flex flex-col md:self-center my-4 px-3 md:px-0 md:mx-4 md:my-1">
      <p class="font-sans text-2xl font-semibold">{{ meal_name }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
const prop = defineProps(["meal_name", "image_link"]);
const img = useImage();
const client = useSupabaseClient();

function newPath(path: string) {
  const segments = path.split("/");
  segments.shift();
  const newPath = segments.join("/");

  return newPath;
}

console.log(prop.image_link);
console.log(newPath(prop.image_link));

const { data } = client.storage
  .from("Meal Images")
  .getPublicUrl(newPath(prop.image_link));

console.log(data.publicUrl);
</script>
