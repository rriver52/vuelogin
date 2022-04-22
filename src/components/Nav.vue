<script setup>
import { useRouter } from "vue-router";
import useAuth from "../composable/useAuth";

const { isAuthenticated, logout } = useAuth();

const router = useRouter();

const loggingOut = () => {
  logout();
  router.push("/");
};
</script>

<template>
  <div class="text-red-200 bg-green-800">
    <div class="container flex items-center justify-between mx-auto">
      <h1 class="font-thin tracking-tighter text-8xl">
        Vue<span class="font-normal">RealAuth</span>
      </h1>
      <nav>
        <ul class="flex space-x-10">
          <router-link to="/">
            <li
              class="px-4 py-8 hover:cursor-pointer hover:bg-pink-500 hover:text-green-800"
            >
              Home
            </li>
          </router-link>
          <router-link :to="{ name: 'About' }">
            <li
              class="px-4 py-8 hover:cursor-pointer hover:bg-pink-500 hover:text-green-800"
            >
              About
            </li>
          </router-link>
          <router-link
            v-if="!isAuthenticated"
            :to="{ path: '/login', name: 'Login' }"
          >
            <li
              class="px-4 py-8 hover:cursor-pointer hover:bg-pink-500 hover:text-green-800"
            >
              Login
            </li>
          </router-link>
          <div v-else class="flex">
            <router-link :to="{ name: 'Secret' }">
              <li
                class="px-4 py-8 hover:cursor-pointer hover:bg-pink-500 hover:text-green-800"
              >
                Secret
              </li>
            </router-link>
            <button @click="loggingOut">
              <li
                class="px-4 py-8 hover:cursor-pointer hover:bg-pink-500 hover:text-green-800"
              >
                Logout
              </li>
            </button>
          </div>
        </ul>
      </nav>
    </div>
  </div>
</template>
