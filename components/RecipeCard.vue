<template>
  <div
    class="flex bg-whitealt shadow-sm hover:shadow-md duration-150 rounded-md border border-gray-200 my-3"
  >
    <div class="h-48 w-48">
      <NuxtImg class="h-48 w-48 object-cover rounded-l-md" src="beef-bulgogi.jpg" />
    </div>
    <div class="flex flex-col self-center mx-6">
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
