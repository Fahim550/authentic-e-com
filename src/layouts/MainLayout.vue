<template>
  <div class="min-h-screen bg-[#f5f6f8]">
    <Navbar @toggle-categories="toggleCategories" />

    <main class="min-w-0 flex-1">
      <RouterView />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import Footer from '@/components/Shared/Footer.vue'
import { computed, ref, watch } from 'vue'
import { RouterView, useRoute } from 'vue-router'
import Navbar from '../components/Shared/Navbar.vue'

const route = useRoute()
const isSidebarVisible = ref(true)
const isHomeRoute = computed(() => route.path === '/')

watch(
  () => route.path,
  (path) => {
    isSidebarVisible.value = path === '/'
  },
  { immediate: true },
)

const toggleCategories = () => {
  if (isHomeRoute.value) {
    isSidebarVisible.value = !isSidebarVisible.value
  }
}
</script>
