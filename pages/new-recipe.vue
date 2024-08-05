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
          v-model="recipe.meal_name"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium mt-2">Description</label>
        <textarea
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 mb-2"
          placeholder="Chicken and rice"
          v-model="recipe.description"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium mt-2">Carbs</label>
        <ul class="flex flex-row flex-wrap justify-center w-full">
          <li v-for="carb in carbsChoices" class="flex m-0.5 grow w-1/4 flex-wrap">
            <input
              type="radio"
              name="Carbs"
              :id="carb"
              class="py-2 mx-1.5 w-5 hidden peer"
              :value="carb"
              v-model="recipe.carbs"
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
              type="radio"
              name="Proteins"
              :id="protein"
              :value="protein"
              v-model="recipe.protein"
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
      <div>
        <label class="block mb-2 mt-2 text-sm font-medium">Any Extra</label>
        <input
          type="text"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5 mb-2"
          placeholder="E.g. Bulgogi sauce required"
          v-model="recipe.extra"
          required
        />
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium text-gray-900 mt-2" for="file_input"
          >Upload an Image</label
        >
        <input
          class="w-full text-blackbg font-medium text-sm bg-white border border-gray-300 file:cursor-pointer cursor-pointer file:border-0 file:py-2.5 file:px-4 file:mr-4 file:bg-blackbg file:hover:bg-black file:text-white rounded-md"
          id="file_input"
          type="file"
          @change="onChangeFile"
        />
      </div>

      <button
        class="bg-blackbg p-1.5 rounded-md w-full text-white mt-4 hover:bg-black"
        @click="submitMeal"
      >
        Create
      </button>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
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
]);
const carbsChoices = ref(["Rice", "Noodles"]);

const recipe = ref({
  meal_name: "",
  description: "",
  carbs: "",
  protein: "",
  extra: "",
  image_link: "",
});

const imagePath = ref("");
const localImage = ref("");

async function onChangeFile(event) {
  localImage.value = event.target.files[0];
}

async function uploadImage() {
  // Upload image
  const { data, error } = await client.storage
    .from("Meal Images")
    .upload("meals/" + localImage.value.name, localImage.value, {
      cacheControl: "3600",
      upsert: false,
    });
  if (error) {
    console.log(error);
  } else {
    recipe.value.image_link = data.fullPath;
  }
}

async function submitMeal() {
  await uploadImage();

  const { error } = await client.from("recipe-list").insert(recipe.value);
  if (error) {
    console.log(error);
  } else {
    navigateTo("/");
  }
}
</script>
