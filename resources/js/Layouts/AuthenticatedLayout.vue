<script setup>
import { Head, usePage } from '@inertiajs/vue3';
import LogoIcon from '@/Components/Icons/LogoIcon.vue';
import UserDropdownMenu from '@/Layouts/Partials/UserDropdownMenu.vue';
import SessionDropdownMenu from '@/Layouts/Partials/SessionDropdownMenu.vue';
import BandIcon from '@/Components/Icons/BandIcon.vue';

defineProps({
  title: String,
});

const user = usePage().props.auth.user;
</script>

<template>
  <Head :title="title" />
  <div>
    <nav class="w-full px-2 md:px-4 py-4 bg-orange-700">
      <div class="max-w-5xl mx-auto flex justify-between items-center">
        <a :href="route('home')" class="hover:cursor-pointer">
          <LogoIcon />
        </a>

        <div class="flex items-center gap-8">
          <a :href="route('bands.index')">
            <BandIcon />
          </a>
          <SessionDropdownMenu />
          <UserDropdownMenu />
        </div>
      </div>
    </nav>

    <main>
      <slot />
    </main>
  </div>
</template>
