<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { useForm, usePage } from '@inertiajs/vue3';
import InputError from '@/Components/InputError.vue';
import { computed } from 'vue';

const props = defineProps({
  spotifyClientId: String,
  spotifyClientSecret: String,
  spotifyRedirectUri: String,
});

const spotifyAuthorizationUrl = computed(() => {
  const scope =
    'user-read-private user-read-email streaming app-remote-control user-read-playback-state';
  const state = 'spotify';

  const params = new URLSearchParams({
    response_type: 'code',
    client_id: props.spotifyClientId,
    scope: scope,
    redirect_uri: props.spotifyRedirectUri,
    state: state,
  }).toString();

  return `https://accounts.spotify.com/authorize?${params}`;
});

const user = usePage().props.auth.user;

const form = useForm({
  first_name: user.first_name,
  last_name: user.last_name,
  username: user.username,
  email: user.email,
});

const submit = () => {
  form.put(route('profile.update'));
};
</script>

<template>
  <AuthenticatedLayout title="Bands">
    <div class="max-w-5xl mx-auto py-12 px-4">
      <div v-if="!user.has_spotify_token" class="mb-4">
        <a
          :href="spotifyAuthorizationUrl"
          class="bg-green-500 text-white px-4 py-2 rounded-lg border border-green-500 hover:bg-green-300 hover:text-green-900 font-bold hover:border-green-300 transition-colors duration-300 ease-in-out hover:cursor-pointer"
        >
          Connect to Spotify
        </a>
      </div>

      <form @submit.prevent="submit" class="space-y-6">
        <div>
          <h3 class="text-orange-700 font-bold text-3xl mb-1">
            Account Settings
          </h3>
          <p class="font-light text-base">
            Manage your account profile details and integration settings.
          </p>
        </div>
        <div>
          <label class="text-lg mb-2" for="first_name">First Name</label>
          <input
            v-model="form.first_name"
            type="text"
            id="first_name"
            class="px-4 py-2 w-full rounded-lg border justify-start items-center gap-2.5 inline-flex text-black placeholder-opacity-10 focus:ring-orange-300 focus:border-orange-300"
            placeholder="Enter your first name..."
          />
          <InputError class="mt-2" :message="form.errors.first_name" />
        </div>
        <div>
          <label class="text-lg mb-2" for="last_name">Last Name</label>
          <input
            v-model="form.last_name"
            type="text"
            id="last_name"
            class="px-4 py-2 w-full rounded-lg border justify-start items-center gap-2.5 inline-flex text-black placeholder-opacity-10 focus:ring-orange-300 focus:border-orange-300"
            placeholder="Enter your last name..."
          />
          <InputError class="mt-2" :message="form.errors.last_name" />
        </div>
        <div>
          <label class="text-lg mb-2" for="username">Username</label>
          <input
            v-model="form.username"
            type="text"
            id="username"
            class="px-4 py-2 w-full rounded-lg border justify-start items-center gap-2.5 inline-flex text-black placeholder-opacity-10 focus:ring-orange-300 focus:border-orange-300"
            placeholder="Enter your username..."
          />
          <InputError class="mt-2" :message="form.errors.username" />
        </div>
        <div>
          <label class="text-lg mb-2" for="email">Email</label>
          <input
            v-model="form.email"
            type="email"
            id="email"
            class="px-4 py-2 w-full rounded-lg border justify-start items-center gap-2.5 inline-flex text-black placeholder-opacity-10 focus:ring-orange-300 focus:border-orange-300"
            placeholder="Enter your email address..."
          />
          <InputError class="mt-2" :message="form.errors.email" />
        </div>
        <div>
          <button
            type="submit"
            class="float-right w-[150px] bg-orange-700 text-white px-4 py-2 rounded-lg border border-orange-700 hover:bg-orange-300 hover:text-orange-900 font-bold hover:border-orange-300 transition-colors duration-300 ease-in-out hover:cursor-pointer"
          >
            Save
          </button>
        </div>
      </form>
    </div>
  </AuthenticatedLayout>
</template>
