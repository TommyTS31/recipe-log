<template>
  <div class="flex justify-around bg-gray-50 shadow-md w-full">
    <div></div>
    <a href="/">
      <div class="p-3">
        <p class="font-title font-regular text-lg font-semibold text-black">Recipe Log</p>
      </div>
    </a>
    <div class="text-white font-sans m-3" v-if="isLoggedIn()">
      <a
        class="bg-blackbg hover:bg-black px-3 py-1 rounded-md shadow-sm"
        href="/new-recipe"
        >Add Recipe</a
      >
      <button class="text-blackbg hover:text-black px-3 py-1" @click="logout">
        Log Out
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
const client = useSupabaseClient();
const {
  data: { user },
} = await client.auth.getUser();

function isLoggedIn() {
  if (user) {
    return true;
  } else {
    return false;
  }
}

async function logout() {
  await client.auth.signOut();
  navigateTo("/login");
}
</script>
