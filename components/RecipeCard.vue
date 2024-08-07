<template>
  <!-- Linear Display Option -->
  <div v-if="displayOption">
    <NuxtLink
      class="flex flex-col md:flex-row bg-whitealt shadow-sm hover:shadow-md hover:border-gray-400 duration-50 rounded-md border border-gray-300 my-1 mx-0.5"
      :to="link"
    >
      <div>
        <NuxtImg
          class="min-w-44 max-h-56 md:min-w-72 md:max-h-64 w-full object-cover rounded-l-md"
          :src="img(data.publicUrl)"
        />
      </div>
      <div class="flex flex-col justify-between my-2 px-3 md:px-0 md:mx-4 md:my-3">
        <p class="font-sans text-md font-medium hover:underline">{{ meal_name }}</p>
        <div class="mt-1 flex flex-col space-y-1 text-xs min-w-32 w-min mb-3">
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ carbs }}</span
          >
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ protein }}</span
          >
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ extra }}</span
          >
        </div>
      </div>
    </NuxtLink>
  </div>
  <!-- Boxy Display Option -->
  <div v-else>
    <NuxtLink
      class="flex flex-col md:flex-row bg-whitealt shadow-sm hover:shadow-md hover:border-gray-400 duration-50 rounded-md border border-gray-300 my-1 mx-1"
      :to="link"
    >
      <div>
        <NuxtImg
          class="min-w-44 max-h-56 md:min-w-44 md:max-h-56 w-full object-cover rounded-l-md"
          :src="img(data.publicUrl)"
        />
      </div>
      <div class="flex flex-col justify-between my-2 px-3 md:px-0 md:mx-4 md:my-3">
        <p class="font-sans text-md font-medium hover:underline">
          {{ meal_name }}
        </p>
        <div class="mt-1 flex flex-col space-y-1 text-xs min-w-32 w-min mb-3">
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ carbs }}</span
          >
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ protein }}</span
          >
          <span
            class="px-2 py-1 rounded-md text-gray-600 border border-gray-300 hover:bg-gray-200"
            >{{ extra }}</span
          >
        </div>
      </div>
    </NuxtLink>
  </div>
</template>

<script setup lang="ts">
const option = ref(false);
const prop = defineProps([
  "meal_name",
  "image_link",
  "carbs",
  "protein",
  "extra",
  "id",
  "displayOption",
]);
const img = useImage();
const client = useSupabaseClient();
const link = "/meal/" + prop.id;

function newPath(path: string) {
  const segments = path.split("/");
  segments.shift();
  const newPath = segments.join("/");
  return newPath;
}
const { data } = client.storage
  .from("Meal Images")
  .getPublicUrl(newPath(prop.image_link));
</script>
