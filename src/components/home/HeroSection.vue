<template>
  <div class="mx-auto bg-white flex flex-row w-full items-start gap-4 px-4 pt-5 sm:px-6 lg:px-14">
    <aside
      class="h-fit w-full max-w-[280px] rounded-xl border border-gray-200 bg-white p-4 shadow-sm lg:h-[460px]"
    >
      <h2 class="mb-3 text-sm font-semibold uppercase tracking-wider text-gray-500">
        Shop By Category
      </h2>
      <ul class="space-y-2">
        <li
          v-for="category in categories"
          :key="category"
          class="flex items-center gap-3 rounded-lg px-3 py-2 text-sm font-medium text-gray-700 transition hover:bg-gray-100"
        >
          <span
            class="inline-flex h-5 w-5 items-center justify-center rounded-md bg-gray-100 text-xs font-semibold text-gray-500"
          >
            •
          </span>
          <span>{{ category }}</span>
        </li>
      </ul>
    </aside>

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
              class="hero-item hero-item-1 text-lg font-semibold uppercase tracking-wider text-rose-500"
            >
              {{ currentBanner.name }}
            </p>

            <h2
              class="hero-item hero-item-2 pt-2 text-gray-900 text-3xl font-extrabold sm:text-4xl lg:text-6xl"
            >
              {{ currentBanner.title }}
            </h2>

            <p class="hero-item hero-item-3 pt-4 pb-5 text-lg font-medium sm:text-2xl">
              {{ saleText.label }}
              <span class="ml-1 text-xl font-bold sm:text-3xl">{{ saleText.value }}</span>
            </p>

            <RouterLink
              to="/shop"
              class="hero-item hero-item-4 max-w-28 inline-block rounded-lg bg-white text-center px-4 py-3 font-semibold text-black transition hover:bg-gray-100"
            >
              Shop Now
            </RouterLink>
          </div>
        </div>
      </article>

      <div class="absolute bottom-8 left-6 z-20 flex gap-3 sm:left-10 md:left-16">
        <button
          v-for="(banner, index) in banners"
          :key="banner._id"
          type="button"
          class="h-3 rounded-full border border-white/50 transition-all duration-300"
          :class="index === currentIndex ? 'w-8 bg-white' : 'w-3 bg-white/50 hover:bg-white/80'"
          :aria-label="`Go to slide ${index + 1}`"
          @click="goTo(index)"
        />
      </div>
    </section>
  </div>
</template>

<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import { RouterLink } from 'vue-router'

const categories = [
  'Headphones',
  'Fashion',
  'Mobile & Tablets',
  'Cosmetics',
  'Furniture',
  'Handbags',
  'Ornaments',
  'Sneakers',
  'Electronics',
  'Game & Console',
]

const banners = [
  {
    _id: '1',
    name: "Women's Clothing Sale",
    title: 'Biggest Promotion At The End Of The Year',
    startFrom: 0,
    image: 'https://i.ibb.co.com/LhtVWSbJ/Gemini-Generated-Image-irx4f6irx4f6irx4.png',
    bannerType: 'hero',
    sale: 'Sale Up To',
    value: '60%',
    weight: 1,
  },
  {
    _id: '2',
    name: 'Audio Deal',
    title: 'Buy 2 Wireless Speakers, Get 1 Free',
    startFrom: 0,
    image: 'https://i.ibb.co.com/ksf9BZFN/Gemini-Generated-Image-350kga350kga350k.png',
    bannerType: 'hero',
    sale: 'Sale Up To',
    value: '30%',
    weight: 2,
  },
  {
    _id: '3',
    name: 'New Arrivals',
    title: 'Premium Home Decor Collection',
    startFrom: 99,
    image: 'https://i.ibb.co.com/j9w3wMqZ/Gemini-Generated-Image-vayr04vayr04vayr.png',
    bannerType: 'hero',
    weight: 3,
  },
]

const currentIndex = ref(0)
let intervalId = null

const currentBanner = computed(() => banners[currentIndex.value] ?? null)

const saleText = computed(() => {
  if (!currentBanner.value) return { label: '', value: '' }

  if (currentBanner.value.sale || currentBanner.value.value) {
    return {
      label: currentBanner.value.sale || '',
      value: currentBanner.value.value || '',
    }
  }

  return {
    label: 'Starting from',
    value: `$${currentBanner.value.startFrom}`,
  }
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
</style>
