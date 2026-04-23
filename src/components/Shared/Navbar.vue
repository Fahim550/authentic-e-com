<template>
  <header class="bg-[#17172b] text-white">
    <div
      class="py-2 px-4 sm:px-6 lg:px-13 flex flex-row justify-between items-center border-b-2 border-gray-800"
    >
      <p class="text-gray-100 text-center text-md font-normal">
        Black Friday Shopping and Small Business Saturday Deals!!!
      </p>
      <div class="flex justify-end items-center gap-3">
        <button type="button" class="hover:text-white">EN</button>
        <button type="button" class="hover:text-white">BDT</button>
      </div>
    </div>

    <div class="mx-auto max-w-7xl px-4 py-4 sm:px-6 lg:px-13">
      <div class="flex flex-col gap-4 lg:flex-row lg:items-center lg:justify-between">
        <RouterLink to="/" class="text-3xl font-extrabold text-white w-3/12">
          Authentic
        </RouterLink>

        <form class="max-w-2xl w-6/12">
          <div class="flex items-center overflow-hidden rounded-md bg-white text-gray-600">
            <input
              type="text"
              placeholder="Search Products..."
              class="w-full bg-transparent px-4 py-3 text-sm outline-none"
            />
            <button type="button" class="border-l border-gray-200 px-4 py-3">
              <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <circle cx="11" cy="11" r="7" stroke-width="1.8" />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="1.8"
                  d="m20 20-3.2-3.2"
                />
              </svg>
            </button>
          </div>
        </form>

        <div class="flex items-end justify-end gap-4 text-sm text-gray-200 w-3/12">
          <button type="button" class="relative hover:text-white">
            <span class="absolute -right-2 -top-2 rounded-full bg-red-500 px-1.5 text-[10px]"
              >3</span
            >
            <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1.8"
                d="M3 4h2l2.5 11h10.8l2-8H7.2"
              />
              <circle cx="10" cy="20" r="1.3" />
              <circle cx="18" cy="20" r="1.3" />
            </svg>
          </button>
          <button type="button" class="relative hover:text-white">
            <span class="absolute -right-2 -top-2 rounded-full bg-red-500 px-1.5 text-[10px]"
              >0</span
            >
            <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1.8"
                d="m12 21-1.7-1.5C5.4 15.2 2 12.2 2 8.5A4.5 4.5 0 0 1 6.5 4C8.2 4 9.8 4.8 11 6.1 12.2 4.8 13.8 4 15.5 4A4.5 4.5 0 0 1 20 8.5c0 3.7-3.4 6.7-8.3 11L12 21Z"
              />
            </svg>
          </button>
          <button type="button" class="hover:text-white">
            <svg class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor">
              <circle cx="12" cy="8" r="4" stroke-width="1.8" />
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="1.8"
                d="M4 21a8 8 0 0 1 16 0"
              />
            </svg>
          </button>
          <p class="leading-tight">
            Welcome<br />
            <span class="font-semibold text-white">Sign In / Register</span>
          </p>
        </div>
      </div>
    </div>

    <div
      class="mx-auto flex max-w-7xl flex-col gap-3 px-4 py-3 sm:px-6 lg:px-13 lg:flex-row lg:items-center lg:gap-8"
    >
      <button
        type="button"
        class="inline-flex items-center gap-3 rounded-md bg-white px-4 py-2 font-medium w-[280px] text-gray-900 cursor-pointer"
        @click="emit('toggle-categories')"
      >
        <svg class="h-4 w-4" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="1.8"
            d="M4 7h16M4 12h16M4 17h16"
          />
        </svg>
        All Categories
      </button>

      <nav class="flex flex-wrap items-center gap-5 text-sm font-medium">
        <RouterLink
          v-for="link in navLinks"
          :key="link.name"
          :to="link.to"
          class="text-gray-200 transition hover:text-white"
          active-class="text-red-500"
        >
          {{ link.name }}
        </RouterLink>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { RouterLink } from 'vue-router'

const emit = defineEmits(['toggle-categories'])

const navLinks = [
  { name: 'Home', to: '/' },
  { name: 'Shop', to: '/shop' },
  { name: 'Features', to: '/features' },
  { name: 'New Arrivals', to: '/new-arrivals' },
  { name: 'Blogs', to: '/blogs' },
  { name: 'About Us', to: '/about' },
  { name: 'Contact Us', to: '/contact' },
]
</script>
