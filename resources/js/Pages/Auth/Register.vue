<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";
import GoogleLogo from "@/Components/GoogleLogo.vue";
import TwitterLogo from "@/Components/TwitterLogo.vue";
import {
  EyeSlashIcon,
  EyeIcon,
  UserIcon,
  EnvelopeIcon,
} from "@heroicons/vue/24/outline";

import { ref } from "vue";

const form = useForm({
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
  terms: false,
});
const passwordVisible = ref(false);
const passwordVisible2 = ref(false);

const submit = () => {
  form.post(route("register"), {
    onFinish: () => form.reset("password", "password_confirmation"),
  });
};

const googleLogin = () => {
  window.location.href = route("google.redirect");
};
const togglePasswordVisibility = () => {
  passwordVisible.value = !passwordVisible.value;
};
const togglePasswordVisibility2 = () => {
  passwordVisible2.value = !passwordVisible2.value;
};
</script>

<template>
  <Head title="Register" />

  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-6">
    <div class="max-w-6xl w-full mx-auto grid grid-cols-1 md:grid-cols-2 gap-8">
      <!-- Left side with image -->
      <div class="hidden md:block rounded-2xl overflow-hidden relative">
        <div class="absolute text-2xl flex left-10 top-10 font-extrabold">
          <p class="text-red-500">Bitz</p>
          <p class="text-white">Mag</p>
        </div>
        <img
          src="/images/woman.jpg"
          alt="Signup"
          class="w-full h-full object-cover"
        />
        <div
          class="absolute bottom-0 left-0 p-8 text-white bg-gradient-to-t from-black/50 to-transparent"
        >
          <h2 class="text-2xl font-bold mb-2">
            Lorem ipsum dolor sit amet consectetur.
          </h2>
          <p class="text-sm opacity-80">
            Lorem ipsum dolor sit amet consectetur. Condimentum nish nam nish
            tempor pellentesque lacus in amet nulla.
          </p>
        </div>
      </div>

      <!-- Right side with form -->
      <div class="bg-white p-8 rounded-2xl shadow-sm">
        <div class="mb-8">
          <h1 class="text-2xl font-bold">Sign Up</h1>
          <p class="text-gray-600 mt-2">
            Enter your credentials to access your account
          </p>
        </div>

        <form @submit.prevent="submit">
          <div class="space-y-6">
            <div>
              <InputLabel for="name" value="Name" class="text-gray-700" />

              <div class="relative flex items-center">
                <TextInput
                  id="name"
                  type="text"
                  class="mt-1 block w-full rounded-md border-gray-300"
                  v-model="form.name"
                  required
                  autofocus
                  autocomplete="name"
                />
                <button
                  type="button"
                  class="absolute right-0 pr-3 flex items-center text-sm leading-5"
                >
                  <component :is="UserIcon" class="h-5 w-5 text-gray-500" />
                </button>
                <InputError class="mt-2" :message="form.errors.name" />
              </div>
            </div>

            <div>
              <InputLabel
                for="email"
                value="Email Address"
                class="text-gray-700"
              />
              <div class="relative flex items-center">
                <TextInput
                  id="email"
                  type="email"
                  class="mt-1 block w-full rounded-md border-gray-300"
                  v-model="form.email"
                  required
                  autocomplete="username"
                />
                <button
                  type="button"
                  class="absolute right-0 pr-3 flex items-center text-sm leading-5"
                >
                  <component :is="EnvelopeIcon" class="h-5 w-5 text-gray-500" />
                </button>
                <InputError class="mt-2" :message="form.errors.email" />
              </div>
            </div>
            <div>
              <InputLabel for="password" value="Password" />

              <div class="relative flex items-center">
                <TextInput
                  id="password"
                  :type="passwordVisible ? 'text' : 'password'"
                  class="mt-1 block w-full pr-10"
                  v-model="form.password"
                  required
                  autocomplete="new-password"
                />
                <button
                  type="button"
                  class="absolute right-0 pr-3 flex items-center text-sm leading-5"
                  @click="togglePasswordVisibility"
                >
                  <component
                    :is="passwordVisible ? EyeSlashIcon : EyeIcon"
                    class="h-5 w-5 text-gray-500"
                  />
                </button>
              </div>

              <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div>
              <InputLabel
                for="password_confirmation"
                value="Confirm Password"
              />
              <div class="relative flex items-center">
                <TextInput
                  id="password_confirmation"
                  :type="passwordVisible2 ? 'text' : 'password'"
                  class="mt-1 block w-full"
                  v-model="form.password_confirmation"
                  required
                  autocomplete="new-password"
                />
                <button
                  type="button"
                  class="absolute right-0 pr-3 flex items-center text-sm leading-5"
                  @click="togglePasswordVisibility2"
                >
                  <component
                    :is="passwordVisible2 ? EyeSlashIcon : EyeIcon"
                    class="h-5 w-5 text-gray-500"
                  />
                </button>
              </div>
              <InputError
                class="mt-2"
                :message="form.errors.password_confirmation"
              />
            </div>

            <div class="flex items-center">
              <input
                v-model="form.terms"
                type="checkbox"
                class="h-4 w-4 rounded border-gray-300 text-orange-600 focus:ring-orange-500"
                required
              />
              <label class="ml-2 block text-sm text-gray-900">
                By registering, you agree to follow
                <a href="#" class="text-orange-600 hover:text-orange-500"
                  >Terms & Conditions</a
                >,
                <a href="#" class="text-orange-600 hover:text-orange-500"
                  >Privacy and Policy</a
                >
              </label>
            </div>

            <PrimaryButton
              class="w-full justify-center bg-orange-500 hover:bg-orange-600"
              :class="{ 'opacity-25': form.processing }"
              :disabled="form.processing"
            >
              Create Account
            </PrimaryButton>

            <div class="relative">
              <div class="absolute inset-0 flex items-center">
                <div class="w-full border-t border-gray-300"></div>
              </div>
              <div class="relative flex justify-center text-sm">
                <span class="bg-white px-2 text-gray-500">Or</span>
              </div>
            </div>

            <div class="grid grid-row-2 gap-3">
              <button
                type="button"
                @click="googleLogin"
                class="flex items-center justify-center px-4 py-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50"
              >
                <GoogleLogo class="w-7 h-6 mr-2" />
                Continue with Google
              </button>

              <button
                type="button"
                class="flex items-center justify-center px-4 py-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50"
              >
                <TwitterLogo class="w-7 h-6 mr-2" />
                Continue with Twitter
              </button>
            </div>

            <p class="text-center text-sm text-gray-600">
              Already have an account?
              <Link
                :href="route('login')"
                class="font-medium text-orange-600 hover:text-orange-500"
              >
                Login
              </Link>
            </p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>