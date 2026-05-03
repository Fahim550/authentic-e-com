<template>
  <div class="flex flex-col lg:flex-row w-full gap-6 bg-white px-4 py-0 sm:px-6 lg:px-14">
    <div
      class="w-full lg:w-2/3 flex gap-4 rounded-2xl overflow-hidden relative shadow-md"
      v-for="(banner, index) in banners"
      :key="banner.id"
      v-show="currentIndex === index"
    >
      <div
        class="absolute md:relative z-10 p-10 xl:p-18 text-primary w-full lg:w-1/2 space-y-3 flex flex-col gap-5 justify-center"
      >
        <p class="text-md uppercase tracking-wider font-semibold text-primary/50">
          {{ banner.subtitle }}
        </p>

        <h2 class="text-3xl font-bold">
          {{ banner.title }}
        </h2>

        <p class="text-md font-semibold text-primary/60">
          {{ banner.description }}
        </p>

        <button
          class="pt-5 px-5 py-3 w-36 border-primary border-[1px] text-primary hover:bg-primary hover:text-white font-semibold rounded-md cursor-pointer"
        >
          {{ banner.buttonText }}
        </button>

        <div class="pt-8 left-6 z-20 flex gap-2 sm:left-10 md:left-16">
          <button
            v-for="(banner, index) in banners"
            :key="banner._id"
            type="button"
            class="h-2.5 rounded-full border border-white/10 transition-all duration-300"
            :class="
              index === currentIndex ? 'w-7 bg-primary' : 'w-2.5 bg-primary/50 hover:bg-primary/80'
            "
            :aria-label="`Go to slide ${index + 1}`"
            @click="goTo(index)"
          />
        </div>
      </div>
      <div
        class="relative rounded-2xl overflow-hidden bg-gray-100 h-[420px] w-full lg:w-1/2 md:p-5"
        :style="{
          backgroundImage: `url(${banner.image})`,
          backgroundSize: 'cover',
          backgroundPosition: 'center',
        }"
      >
        <div class="md:hidden absolute w-full h-full bg-white/90 backdrop-blur-xl" />
      </div>
    </div>

    <div
      class="w-full lg:w-1/3 rounded-2xl p-8 flex flex-col justify-between shadow-md overflow-hidden relative min-h-[420px]"
    >
      <div
        class="absolute bottom-0 left-0 right-0 h-2/4"
        :style="{
          backgroundImage: `url(${cyberSale.image})`,
          backgroundSize: '',
          backgroundPosition: 'top center',
        }"
      >
        <div
          class="absolute inset-0 bg-gradient-to-b from-accent/15 via-accent/10 to-transparent"
        />
      </div>

      <div class="absolute top-0 left-0 right-0 h-2/4 bg-accent/15" />

      <!-- Content -->
      <div class="relative z-10 pt-2">
        <h2 class="text-3xl font-bold text-center text-primary">Cyber Sale</h2>
        <p class="text-center text-sm font-semibold text-primary/70 pt-5">
          {{ cyberSale.description }}
        </p>

        <!-- Countdown -->
        <div class="flex justify-center gap-5 xl:gap-7 pt-7">
          <div v-for="(item, i) in countdown" :key="i" class="text-center">
            <div
              class="bg-primary text-white w-14 h-14 flex items-center justify-center rounded-full font-bold"
            >
              {{ item.value }}
            </div>
            <p class="text-xs text-primary font-semibold pt-2">{{ item.label }}</p>
          </div>
        </div>
      </div>

      <!-- Shop Now button -->
      <div class="relative z-10 pt-6 justify-center flex">
        <button
          class="bg-white/70 px-6 py-3 rounded-md shadow font-semibold text-primary hover:bg-white/90 transition-colors cursor-pointer"
        >
          Shop Now
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const banners = ref([])
const cyberSale = ref({})
const countdown = ref([])
const currentIndex = ref(0)

let countdownInterval = null
let bannerInterval = null

const formatCountdownValue = (value) => {
  return String(value).padStart(2, '0')
}

const calculateCountdown = (endDate) => {
  const now = new Date().getTime()
  const distance = new Date(endDate).getTime() - now

  if (distance <= 0) {
    countdown.value = [
      { label: 'DAYS', value: 0 },
      { label: 'HRS', value: 0 },
      { label: 'MINS', value: 0 },
      { label: 'SECS', value: 0 },
    ]
    return
  }

  const days = Math.floor(distance / (1000 * 60 * 60 * 24))
  const hours = Math.floor((distance / (1000 * 60 * 60)) % 24)
  const minutes = Math.floor((distance / (1000 * 60)) % 60)
  const seconds = Math.floor((distance / 1000) % 60)

  countdown.value = [
    { label: 'DAYS', value: days },
    { label: 'HRS', value: hours },
    { label: 'MINS', value: minutes },
    { label: 'SECS', value: seconds },
  ]
}

const goTo = (index) => {
  currentIndex.value = index
}

onMounted(() => {
  banners.value = bannerData
  cyberSale.value = cyberSaleData

  calculateCountdown(cyberSale.value.endDate)

  countdownInterval = setInterval(() => {
    calculateCountdown(cyberSale.value.endDate)
  }, 1000)

  bannerInterval = setInterval(() => {
    if (banners.value.length > 0) {
      currentIndex.value = (currentIndex.value + 1) % banners.value.length
    }
  }, 4000)
})

onUnmounted(() => {
  if (countdownInterval) clearInterval(countdownInterval)
  if (bannerInterval) clearInterval(bannerInterval)
})

const bannerData = [
  {
    id: 1,
    subtitle: 'SUMMER DEAL',
    title: 'New Trendy Collection',
    description: 'Up to 40% off',
    buttonText: 'Explore',
    image: 'https://i.pinimg.com/1200x/0e/8a/de/0e8ade5489d2885b29be0c219cfdfca1.jpg',
  },
  {
    id: 2,
    subtitle: 'BLACK FRIDAY SALE',
    title: 'Hooded Jackets For Women',
    description: '10% discount for first customers',
    buttonText: 'Shop Now',
    image: 'https://i.pinimg.com/736x/a9/c8/ab/a9c8abe2fe655aa90cc4d05198718926.jpg',
  },
]

const cyberSaleData = {
  title: 'Cyber Sale',
  description: '20% Off when buying and paying online',
  endDate: '2026-12-31T23:59:59',
  image: 'https://i.pinimg.com/736x/f7/aa/fe/f7aafe5f79f64ad970dfe455357e7562.jpg',
}
</script>
