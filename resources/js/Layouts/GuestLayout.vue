<script setup>
import { Head } from '@inertiajs/vue3';
import LogoIcon from '@/Components/Icons/LogoIcon.vue';

defineProps({
  title: String,
});
</script>

<template>
  <Head :title="title" />
  <div>
    <nav class="w-full px-4 py-4 bg-orange-700 flex justify-center">
      <a :href="route('home')" class="hover:cursor-pointer">
        <LogoIcon />
      </a>
    </nav>

    <main class="bg-container">
      <slot />
    </main>
  </div>
</template>

<style scoped>
.bg-container {
  background-image: url('/images/auth_background.jpg');
  background-size: cover;
  background-position: center;
  min-height: calc(100vh - 4rem);
  display: flex;
  justify-content: center;
}
</style>
