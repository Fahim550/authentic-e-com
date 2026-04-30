<template>
  <div class="mx-auto w-full px-4 sm:px-6 lg:px-13">
    <div class="flex w-full items-start gap-4">
      <aside
        class="hidden lg:block w-72 shrink-0 self-stretch rounded-t-none rounded-b-xl border border-gray-200 bg-white shadow-sm overflow-hidden"
      >
        <div class="p-3">
          <CategoryList />
        </div>
      </aside>

      <!-- Hero Slider -->
      <div class="pt-8 w-full">
        <section
          class="relative h-[310px] w-full overflow-hidden rounded-2xl bg-gray-100 sm:h-[360px] lg:h-[460px]"
        >
          <article
            v-if="currentBanner"
            :key="currentBanner._id"
            class="absolute inset-0"
            :style="{
              backgroundImage: `url(${currentBanner.image})`,
              backgroundSize: 'cover',
              backgroundPosition: 'center',
            }"
          >
            <div class="absolute inset-0 bg-black/20" />
            <div class="relative z-10 flex h-full items-center px-6 sm:px-10 md:px-16">
              <div class="max-w-xl text-white flex flex-col gap-0">
                <p
                  class="hero-item hero-item-1 text-lg font-semibold uppercase tracking-wider text-rose-400"
                >
                  {{ currentBanner.name }}
                </p>
                <h2
                  class="hero-item hero-item-2 pt-2 text-white text-3xl font-extrabold sm:text-4xl lg:text-5xl leading-tight drop-shadow"
                >
                  {{ currentBanner.title }}
                </h2>
                <p class="hero-item hero-item-3 pt-4 pb-5 text-lg font-medium sm:text-2xl">
                  {{ saleText.label }}
                  <span class="ml-1 text-xl font-bold sm:text-3xl text-yellow-300">{{
                    saleText.value
                  }}</span>
                </p>
                <RouterLink
                  to="/shop"
                  class="hero-item hero-item-4 w-fit inline-block rounded-lg bg-white text-center px-6 py-3 font-semibold text-black transition hover:bg-gray-100 shadow"
                >
                  Shop Now
                </RouterLink>
              </div>
            </div>
          </article>

          <!-- Dot indicators -->
          <div class="absolute bottom-6 left-6 z-20 flex gap-2 sm:left-10 md:left-16">
            <button
              v-for="(banner, index) in banners"
              :key="banner._id"
              type="button"
              class="h-2.5 rounded-full border border-white/50 transition-all duration-300"
              :class="
                index === currentIndex ? 'w-7 bg-white' : 'w-2.5 bg-white/50 hover:bg-white/80'
              "
              :aria-label="`Go to slide ${index + 1}`"
              @click="goTo(index)"
            />
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup>
import CategoryList from '@/components/Shared/CategoryList.vue'
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import { RouterLink } from 'vue-router'

const banners = [
  {
    _id: '1',
    name: "Women's Clothing Sale",
    title: 'Biggest Promotion At The End Of The Year',
    startFrom: 0,
    image: 'https://i.ibb.co.com/LhtVWSbJ/Gemini-Generated-Image-irx4f6irx4f6irx4.png',
    sale: 'Sale Up To',
    value: '60%',
  },
  {
    _id: '2',
    name: 'Audio Deal',
    title: 'Buy 2 Wireless Speakers, Get 1 Free',
    startFrom: 0,
    image: 'https://i.ibb.co.com/ksf9BZFN/Gemini-Generated-Image-350kga350kga350k.png',
    sale: 'Sale Up To',
    value: '30%',
  },
  {
    _id: '3',
    name: 'New Arrivals',
    title: 'Premium Home Decor Collection',
    startFrom: 99,
    image: 'https://i.ibb.co.com/j9w3wMqZ/Gemini-Generated-Image-vayr04vayr04vayr.png',
  },
]

const currentIndex = ref(0)
let intervalId = null

const currentBanner = computed(() => banners[currentIndex.value] ?? null)

const saleText = computed(() => {
  if (!currentBanner.value) return { label: '', value: '' }
  if (currentBanner.value.sale || currentBanner.value.value) {
    return { label: currentBanner.value.sale || '', value: currentBanner.value.value || '' }
  }
  return { label: 'Starting from', value: `$${currentBanner.value.startFrom}` }
})

const goTo = (index) => {
  currentIndex.value = index
}

onMounted(() => {
  if (banners.length <= 1) return
  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % banners.length
  }, 5000)
})

onBeforeUnmount(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<style scoped>
/* Hero animations */
.hero-item {
  opacity: 0;
  animation: slide-left-in 0.55s ease-out forwards;
}
.hero-item-1 {
  animation-delay: 0.12s;
}
.hero-item-2 {
  animation-delay: 0.2s;
}
.hero-item-3 {
  animation-delay: 0.28s;
}
.hero-item-4 {
  animation-delay: 0.36s;
}

@keyframes slide-left-in {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Drawer backdrop fade */
.drawer-fade-enter-active,
.drawer-fade-leave-active {
  transition: opacity 0.25s ease;
}
.drawer-fade-enter-from,
.drawer-fade-leave-to {
  opacity: 0;
}

/* Drawer panel slide */
.drawer-slide-enter-active,
.drawer-slide-leave-active {
  transition: transform 0.28s cubic-bezier(0.4, 0, 0.2, 1);
}
.drawer-slide-enter-from,
.drawer-slide-leave-to {
  transform: translateX(-100%);
}
</style>
