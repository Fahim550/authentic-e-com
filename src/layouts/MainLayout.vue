<template>
  <div class="min-h-screen bg-[#f5f6f8]">
    <Navbar @toggle-categories="toggleCategories" />
    <!-- <div class="mx-auto  w-full items-start gap-4 px-4 py-5 sm:px-6 lg:px-14">
      <aside
        v-if="isHomeRoute && isSidebarVisible"
        class="h-fit w-full max-w-[280px] rounded-xl border border-gray-200 bg-white p-4 shadow-sm lg:h-[460px]"
      >
        <h2 class="mb-3 text-sm font-semibold uppercase tracking-wider text-gray-500">Shop By Category</h2>
        <ul class="space-y-2">
          <li
            v-for="category in categories"
            :key="category"
            class="flex items-center gap-3 rounded-lg px-3 py-2 text-sm font-medium text-gray-700 transition hover:bg-gray-100"
          >
            <span class="inline-flex h-5 w-5 items-center justify-center rounded-md bg-gray-100 text-xs font-semibold text-gray-500">
              •
            </span>
            <span>{{ category }}</span>
          </li>
        </ul>
      </aside> -->

      <main class="min-w-0 flex-1">
        <RouterView />
      </main>
    <!-- </div> -->
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';
import { RouterView, useRoute } from 'vue-router';
import Navbar from '../components/Shared/Navbar.vue';

const route = useRoute();
const isSidebarVisible = ref(true);
const isHomeRoute = computed(() => route.path === '/');



watch(
  () => route.path,
  (path) => {
    isSidebarVisible.value = path === '/';
  },
  { immediate: true },
);

const toggleCategories = () => {
  if (isHomeRoute.value) {
    isSidebarVisible.value = !isSidebarVisible.value;
  }
};
</script>