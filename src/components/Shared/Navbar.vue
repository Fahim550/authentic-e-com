<template>
  <header class="bg-primary text-text-inverse">
    <div
      class="py-3 px-4 sm:px-6 lg:px-13 flex flex-row justify-between items-center border-b-[1px] border-border-strong gap-2"
    >
      <p class="text-foreground text-sm font-semibold tracking-wider truncate flex-1 min-w-0">
        Black Friday Shopping
        <span class="hidden sm:inline"> and Small Business Saturday Deals!!! </span>
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
      <div class="flex items-center justify-between gap-4 py-2">
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
              class="w-full bg-transparent text-black px-4 py-3.5 text-sm outline-none"
            />
            <button
              type="submit"
              class="border-l text-black border-gray-200 px-4 py-2 hover:bg-gray-100 transition cursor-pointer"
            >
              <Search class="h-7 w-7" />
            </button>
          </div>
        </form>

        <div class="flex items-center gap-4 sm:gap-6 text-gray-200 shrink-0">
          <button
            type="button"
            class="md:hidden hover:text-white transition"
            @click="searchOpen = !searchOpen"
          >
            <Search class="h-7 w-7" />
          </button>

          <button type="button" class="relative hover:text-foreground transition cursor-pointer">
            <span
              class="absolute -right-5 -top-5 rounded-full bg-accent px-3 py-2 text-[10px] leading-4"
              >3</span
            >
            <ShoppingCart class="h-8 w-8" />
          </button>

          <button type="button" class="relative hover:text-foreground transition cursor-pointer">
            <span
              class="absolute -right-5 -top-5 rounded-full bg-accent px-3 py-2 text-[10px] leading-4"
              >0</span
            >
            <Heart class="h-8 w-8" />
          </button>

          <div class="hidden sm:flex items-center gap-2">
            <button type="button" class="hover:text-foreground transition cursor-pointer">
              <User class="h-8 w-8" />
            </button>
            <p class="leading-tight text-sm text-left">
              Welcome<br />
              <span class="font-normal text-foreground">Sign In / Register</span>
            </p>
          </div>

          <button
            type="button"
            class="lg:hidden hover:text-foreground transition ml-1"
            @click="mobileMenuOpen = !mobileMenuOpen"
            aria-label="Toggle menu"
          >
            <X v-if="mobileMenuOpen" class="h-7 w-7" />
            <Menu v-else class="h-7 w-7" />
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
              <Search class="h-6 w-6" />
            </button>
          </div>
        </div>
      </Transition>
    </div>

    <!-- Nav Bar -->
    <div class="max-w-7xl px-4 pt-3 sm:px-6 lg:px-13">
      <!-- Desktop Nav -->
      <div class="relative md:flex items-center gap-4">
        <div>
          <button
            type="button"
            class="inline-flex items-center gap-3 rounded-t-xl rounded-b-none bg-white px-6 py-3 font-semibold text-md w-64 lg:w-72 text-primary cursor-pointer hover:bg-gray-100 transition shrink-0"
            @click="(toggleSidebar(), (mobileMenuOpen = false))"
          >
            <LayoutGrid class="h-6 w-6" />
            All Categories
          </button>

          <Transition name="fade">
            <div v-if="sidebarOpen" class="lg:hidden absolute z-[10001]">
              <div
                class="w-64 lg:w-72 bg-white rounded-b-xl shadow-2xl border border-gray-200 overflow-hidden"
              >
                <div
                  v-if="sidebarOpen"
                  class="lg:hidden fixed inset-0 z-[10000]"
                  @click="closeSidebar"
                />
                <div class="h-full overflow-y-auto p-3">
                  <CategoryList @select="closeSidebar" />
                </div>
              </div>
            </div>
          </Transition>
        </div>

        <nav class="hidden md:flex items-center gap-5 lg:gap-7 xl:gap-10 lg:px-4">
          <RouterLink
            v-for="link in navLinks"
            :key="link.name"
            :to="link.to"
            :class="[
              'transition  lg:max-w-none text-md font-family-primary font-semibold',
              $route.path === link.to ? 'text-accent' : 'text-foreground',
            ]"
          >
            {{ link.name }}
          </RouterLink>
        </nav>
      </div>

      <!-- Mobile Nav Dropdown -->
      <Transition name="slide-down">
        <div v-if="mobileMenuOpen" class="lg:hidden flex flex-col gap-1 pt-1">
          <div class="sm:hidden flex items-center gap-2 py-2 border-b border-white/10 mb-1">
            <User class="h-4 w-4 text-foreground" />
            <span class="text-sm text-foreground text-start"
              >Welcome — <span class="font-semibold text-white">Sign In / Register</span></span
            >
          </div>

          <nav
            :class="[
              'flex flex-col',
              isScrolled
                ? 'fixed top-13 sm:top-19 left-0 right-0 z-[9998] bg-primary px-4 transition-all duration-300'
                : 'relative',
            ]"
          >
            <RouterLink
              v-for="link in navLinks"
              :key="link.name"
              :to="link.to"
              :class="[
                'text-gray-200 hover:text-white transition py-2.5 border-b border-white/10 text-md font-semibold',
                $route.path === link.to ? 'text-accent' : 'text-foreground',
              ]"
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

.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
