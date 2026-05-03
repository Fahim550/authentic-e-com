<template>
  <section class="px-4 py-10 sm:px-6 lg:px-14 bg-white">
    <!-- Header -->
    <div class="flex items-center justify-between mb-8">
      <h2 class="text-2xl font-bold text-primary sm:text-3xl">Shop By Brands</h2>

      <div class="flex items-center gap-4">
        <button
          @click="prev"
          :disabled="currentIndex === 0"
          class="z-10 -translate-y-1/2 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-lg border border-gray-800 text-primary transition hover:bg-primary hover:text-white disabled:opacity-30 disabled:cursor-not-allowed cursor-pointer"
          aria-label="Previous"
        >
          <ChevronLeft class="h-6 w-6" />
        </button>

        <button
          @click="next"
          :disabled="currentIndex >= maxIndex"
          class="-translate-y-1/2 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-lg border border-gray-800 text-primary transition hover:bg-primary hover:text-white disabled:opacity-30 disabled:cursor-not-allowed cursor-pointer"
          aria-label="Next"
        >
          <ChevronRight class="h-6 w-6" />
        </button>
      </div>
    </div>

    <div class="overflow-hidden" ref="sliderRef">
      <div
        class="flex gap-4 transition-transform duration-500 ease-in-out"
        :style="{ transform: `translateX(-${currentIndex * slideWidth}px)` }"
      >
        <div
          v-for="brand in brands"
          :key="brand.id"
          class="flex-shrink-0 flex flex-col items-center gap-3 cursor-pointer group"
          :style="{ width: `${cardWidth}px` }"
        >
          <div
            class="w-full aspect-square rounded-full border border-gray-200 flex items-center justify-center bg-white group-hover:border-gray-400 group-hover:shadow-md transition-all duration-200 p-8"
          >
            <img :src="brand.logo" :alt="brand.name" class="w-full h-full object-contain" />
          </div>
          <span
            class="text-sm text-primary/80 text-center group-hover:text-primary font-semibold transition-colors"
          >
            {{ brand.name }}
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ChevronLeft, ChevronRight } from '@lucide/vue'
import { computed, onMounted, onUnmounted, ref } from 'vue'

const brands = ref([
  {
    id: 1,
    name: 'Sony',
    logo: 'https://upload.wikimedia.org/wikipedia/commons/c/ca/Sony_logo.svg',
  },
  {
    id: 2,
    name: 'HiKoKi',
    logo: 'https://images.seeklogo.com/logo-png/40/1/hikoki-logo-png_seeklogo-400173.png',
  },
  {
    id: 15,
    name: 'Hp',
    logo: 'https://i.pinimg.com/736x/da/fc/39/dafc39a5027003313bf3a435ffe50787.jpg',
  },
  {
    id: 16,
    name: 'Asus',
    logo: 'https://i.pinimg.com/1200x/86/e0/50/86e05042b9fae73b0c12517ee5cef558.jpg',
  },
  {
    id: 3,
    name: 'Samsung',
    logo: 'https://www.svgrepo.com/show/303265/samsung-logo.svg',
  },
  {
    id: 4,
    name: 'LG Electronics',
    logo: 'https://images.squarespace-cdn.com/content/v1/502a8efb84ae42cbccf920c4/1585574686746-VCDIHSO21O76WR72WIAD/LG-Logo.png?format=1500w',
  },
  {
    id: 5,
    name: 'Huawei',
    logo: 'https://images.seeklogo.com/logo-png/6/1/huawei-logo-png_seeklogo-68529.png',
  },
  {
    id: 6,
    name: 'Vivo',
    logo: 'https://upload.wikimedia.org/wikipedia/commons/1/13/Vivo_logo_2019.svg',
  },
  {
    id: 7,
    name: 'Apple',
    logo: 'https://i.pinimg.com/736x/80/75/b6/8075b665a68076d7ebcb5618197c7da2.jpg',
  },
  {
    id: 8,
    name: 'Xiaomi',
    logo: 'https://i.pinimg.com/1200x/0a/06/57/0a06573f82b48bd48f95e4a4e5dc4ca2.jpg',
  },
  {
    id: 9,
    name: 'Lenovo',
    logo: 'https://upload.wikimedia.org/wikipedia/commons/b/b8/Lenovo_logo_2015.svg',
  },
  {
    id: 10,
    name: 'Dell',
    logo: 'https://upload.wikimedia.org/wikipedia/commons/8/82/Dell_Logo.png',
  },
])

const sliderRef = ref(null)
const currentIndex = ref(0)
const visibleCount = ref(7)
const gap = 16

const cardWidth = computed(() => {
  if (!sliderRef.value) return 150
  return (sliderRef.value.offsetWidth - gap * (visibleCount.value - 1)) / visibleCount.value
})

const slideWidth = computed(() => cardWidth.value + gap)

const maxIndex = computed(() => Math.max(0, brands.value.length - visibleCount.value))

const updateVisibleCount = () => {
  const w = window.innerWidth
  if (w < 480) visibleCount.value = 2
  else if (w < 640) visibleCount.value = 3
  else if (w < 768) visibleCount.value = 4
  else if (w < 1024) visibleCount.value = 5
  else visibleCount.value = 7

  // clamp currentIndex after resize
  if (currentIndex.value > maxIndex.value) {
    currentIndex.value = maxIndex.value
  }
}

const prev = () => {
  if (currentIndex.value > 0) currentIndex.value--
}

const next = () => {
  if (currentIndex.value < maxIndex.value) currentIndex.value++
}

onMounted(() => {
  updateVisibleCount()
  window.addEventListener('resize', updateVisibleCount)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateVisibleCount)
})
</script>
