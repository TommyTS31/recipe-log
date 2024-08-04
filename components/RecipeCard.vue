<template>
  <div
    class="flex flex-col md:flex-row bg-whitealt shadow-sm hover:shadow-md duration-150 rounded-md border border-gray-200 my-3 mx-0 md:mx-1"
  >
    <div>
      <NuxtImg
        class="h-72 md:h-48 md:w-48 w-full object-cover rounded-l-md"
        src="beef-bulgogi.jpg"
      />
    </div>
    <div class="flex flex-col self-center my-4 mx-2 md:mx-6 md:my-1">
      <p class="font-sans text-3xl font-semibold">Ground Beef Bulogi with Rice</p>
      <div class="flex flex-row">
        <span
          class="bg-blue-400 mx-1 rounded-sm text-blue-800 px-1.5 py-0.5"
          v-for="n in 4"
          >Beef</span
        >
      </div>
    </div>
  </div>
</template>
