<template>
  <header class="bg-primary text-text-inverse">
    <div
      class="py-3 px-4 sm:px-6 lg:px-13 flex flex-row justify-between items-center border-b border-border-strong gap-2"
    >
      <p class="text-foreground text-sm font-normal truncate flex-1 min-w-0">
        Black Friday Shopping and Small Business Saturday Deals!!!
      </p>
      <div class="flex items-center gap-3 shrink-0">
        <button
          type="button"
          class="text-foreground text-sm hover:opacity-80 transition cursor-pointer"
        >
          EN
        </button>
        <button
          type="button"
          class="text-foreground text-sm hover:opacity-80 transition cursor-pointer"
        >
          BDT
        </button>
        <!-- <a href="#" class="text-foreground hover:text-blue-500 transition">
          <Facebook class="h-4 w-4" />
        </a>
        <a href="#" class="text-foreground hover:text-blue-600 transition">
          <Linkedin class="h-4 w-4" />
        </a>
        <a href="#" class="text-foreground hover:text-pink-500 transition">
          <Instagram class="h-4 w-4" />
        </a> -->
      </div>
    </div>

    <!-- Main Header -->
    <div
      :class="[
        'mx-auto  text-center px-4 py-2 sm:px-6 lg:px-12 transition-all duration-400',
        isScrolled
          ? 'fixed top-0 left-0 right-0 z-[9999] bg-primary shadow-md py-3'
          : 'relative py-4',
      ]"
    >
      <div class="flex items-center justify-between gap-4">
        <RouterLink
          to="/"
          class="text-xl sm:text-2xl lg:text-3xl font-extrabold text-foreground shrink-0"
        >
          Authentic
        </RouterLink>

        <form class="hidden md:flex flex-1 max-w-2xl" @submit.prevent>
          <div
            class="flex w-full items-center overflow-hidden rounded-md bg-background text-foreground border border-border"
          >
            <input
              type="text"
              placeholder="Search Products..."
              class="w-full bg-transparent text-black px-4 py-2.5 text-sm outline-none"
            />
            <button
              type="submit"
              class="border-l text-black border-gray-200 px-4 py-2.5 hover:bg-gray-100 transition cursor-pointer"
            >
              <Search class="h-5 w-5" />
            </button>
          </div>
        </form>

        <div class="flex items-center gap-3 sm:gap-4 text-gray-200 shrink-0">
          <button
            type="button"
            class="md:hidden hover:text-white transition"
            @click="searchOpen = !searchOpen"
          >
            <Search class="h-5 w-5" />
          </button>

          <button type="button" class="relative hover:text-white transition cursor-pointer">
            <span
              class="absolute -right-2 -top-2 rounded-full bg-red-500 px-1.5 text-[10px] leading-4"
              >3</span
            >
            <ShoppingCart class="h-5 w-5" />
          </button>

          <button type="button" class="relative hover:text-white transition cursor-pointer">
            <span
              class="absolute -right-2 -top-2 rounded-full bg-red-500 px-1.5 text-[10px] leading-4"
              >0</span
            >
            <Heart class="h-5 w-5" />
          </button>

          <div class="hidden sm:flex items-center gap-2">
            <button type="button" class="hover:text-white transition cursor-pointer">
              <User class="h-5 w-5" />
            </button>
            <p class="leading-tight text-sm">
              Welcome<br />
              <span class="font-semibold text-white">Sign In / Register</span>
            </p>
          </div>

          <button
            type="button"
            class="lg:hidden hover:text-white transition ml-1"
            @click="mobileMenuOpen = !mobileMenuOpen"
            aria-label="Toggle menu"
          >
            <X v-if="mobileMenuOpen" class="h-6 w-6" />
            <Menu v-else class="h-6 w-6" />
          </button>
        </div>
      </div>

      <!-- Mobile Search -->
      <Transition name="slide-down">
        <div v-if="searchOpen" class="mt-3 md:hidden">
          <div
            class="flex items-center overflow-hidden rounded-md bg-background text-foreground border border-border"
          >
            <input
              type="text"
              placeholder="Search Products..."
              class="w-full text-black bg-transparent px-4 py-2.5 text-sm outline-none"
              autofocus
            />
            <button type="button" class="border-l text-black border-gray-200 px-4 py-2.5">
              <Search class="h-5 w-5" />
            </button>
          </div>
        </div>
      </Transition>
    </div>

    <!-- Nav Bar -->
    <div class="mx-auto max-w-7xl px-4 pt-3 sm:px-6 lg:px-13">
      <!-- Desktop Nav -->
      <div class="md:flex items-center gap-4">
        <button
          type="button"
          class="inline-flex items-center gap-3 rounded-t-xl rounded-b-none bg-white px-4 py-2 font-medium w-72 text-gray-900 cursor-pointer hover:bg-gray-100 transition shrink-0"
          @click="(toggleSidebar(), (mobileMenuOpen = false))"
        >
          <LayoutGrid class="h-4 w-4" />
          All Categories
        </button>

        <Transition name="fade">
          <div v-if="sidebarOpen" class="lg:hidden absolute z-[9999] mt-2">
            <div
              class="w-72 bg-white rounded-b-xl shadow-2xl border border-gray-200 overflow-hidden"
            >
              <div class="h-full overflow-y-auto p-3">
                <CategoryList @select="closeSidebar" />
              </div>
            </div>
          </div>
        </Transition>

        <nav class="hidden md:flex flex-wrap items-center gap-5 lg:gap-6 text-sm font-bold">
          <RouterLink
            v-for="link in navLinks"
            :key="link.name"
            :to="link.to"
            class="text-gray-200 transition max-w-12 lg:max-w-none text-md font-bold hover:text-white"
            active-class="text-red-400"
          >
            {{ link.name }}
          </RouterLink>
        </nav>
      </div>

      <!-- Mobile Nav Dropdown -->
      <Transition name="slide-down">
        <div v-if="mobileMenuOpen" class="lg:hidden flex flex-col gap-1 pt-1">
          <div class="sm:hidden flex items-center gap-2 py-2 border-b border-white/10 mb-1">
            <User class="h-4 w-4 text-gray-300" />
            <span class="text-sm text-gray-200"
              >Welcome — <span class="font-semibold text-white">Sign In / Register</span></span
            >
          </div>

          <nav class="flex flex-col">
            <RouterLink
              v-for="link in navLinks"
              :key="link.name"
              :to="link.to"
              class="text-gray-200 hover:text-white transition py-2.5 border-b border-white/10 text-md font-semibold"
              active-class="text-red-400"
              @click="mobileMenuOpen = false"
            >
              {{ link.name }}
            </RouterLink>
          </nav>
        </div>
      </Transition>
    </div>
  </header>
</template>

<script setup>
import CategoryList from '@/components/Shared/CategoryList.vue'
import { useSidebar } from '@/composables/useSidebar'
import { Heart, LayoutGrid, Menu, Search, ShoppingCart, User, X } from '@lucide/vue'
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { RouterLink } from 'vue-router'

const { toggleSidebar } = useSidebar()
const { sidebarOpen, closeSidebar } = useSidebar()

const mobileMenuOpen = ref(false)
const searchOpen = ref(false)

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll)
})

const navLinks = [
  { name: 'Home', to: '/' },
  { name: 'Shop', to: '/shop' },
  { name: 'Features', to: '/features' },
  { name: 'New Arrivals', to: '/new-arrivals' },
  { name: 'Blogs', to: '/blogs' },
  { name: 'About ', to: '/about' },
  { name: 'Contact ', to: '/contact' },
]
</script>

<style scoped>
.slide-down-enter-active,
.slide-down-leave-active {
  transition: all 0.2s ease;
}
.slide-down-enter-from,
.slide-down-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
