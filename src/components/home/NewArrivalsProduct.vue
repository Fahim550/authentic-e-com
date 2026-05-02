<template>
  <section class="mx-auto w-full rounded-2xl bg-white px-4 py-6 sm:px-6 lg:px-14">
    <div class="flex flex-wrap items-end justify-between gap-3 pb-4">
      <div>
        <h2 class="mt-1 text-2xl font-bold text-primary sm:text-3xl">New Arrivals</h2>
      </div>
      <a href="#" class="text-sm font-semibold text-primary hover:underline">View More</a>
    </div>

    <div class="relative mt-8">
      <!-- <div class="mt-8 grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-4"> -->
      <div ref="emblaRef" class="overflow-hidden">
        <div class="flex gap-3">
          <Product
            v-for="item in featuredProducts"
            :key="item.id"
            :title="item.title"
            :category="item.category"
            :image="item.image"
            :price="item.price"
            :old-price="item.oldPrice"
            :rating="item.rating"
            :badge="item.badge"
            class="min-w-0 flex-[0_0_100%] sm:flex-[0_0_49%] lg:flex-[0_0_24.5%]"
          />
        </div>
      </div>

      <!-- Prev Button — vertically centered on the carousel -->
      <button
        @click="scrollPrev"
        :disabled="!canScrollPrev"
        class="absolute left-0 top-1/2 z-10 -translate-x-1/2 -translate-y-1/2 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-lg border border-gray-800 text-primary transition hover:bg-primary hover:text-white disabled:opacity-30 disabled:cursor-not-allowed cursor-pointer"
        aria-label="Previous"
      >
        <ChevronLeft class="h-6 w-6" />
      </button>

      <!-- Next Button -->
      <button
        @click="scrollNext"
        :disabled="!canScrollNext"
        class="absolute right-0 top-1/2 z-10 translate-x-1/2 -translate-y-1/2 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-lg border border-gray-800 text-primary transition hover:bg-primary hover:text-white disabled:opacity-30 disabled:cursor-not-allowed cursor-pointer"
        aria-label="Next"
      >
        <ChevronRight class="h-6 w-6" />
      </button>
    </div>
  </section>
</template>

<script setup>
import { ChevronLeft, ChevronRight } from '@lucide/vue'
import emblaCarouselVue from 'embla-carousel-vue'
import { onBeforeUnmount, onMounted, ref } from 'vue'
import Product from '../Shared/Product.vue'

const featuredProducts = [
  {
    id: 1,
    title: 'Sony WH-1000XM5 Wireless Headphones',
    category: 'Audio',
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?auto=format&fit=crop&w=900&q=80',
    price: 339.99,
    oldPrice: 399.99,
    rating: 4.8,
    badge: '20% OFF',
  },
  {
    id: 6,
    title: 'Sony WH-1000XM5 Wireless Headphones',
    category: 'Audio',
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?auto=format&fit=crop&w=900&q=80',
    price: 339.99,
    oldPrice: 399.99,
    rating: 4.8,
    badge: '20% OFF',
  },
  {
    id: 2,
    title: 'Apple Watch Series 9 GPS 45mm',
    category: 'Wearables',
    image:
      'https://images.unsplash.com/photo-1546868871-7041f2a55e12?auto=format&fit=crop&w=900&q=80',
    price: 429.0,
    oldPrice: 499.0,
    rating: 4.7,
    badge: 'Hot',
  },
  {
    id: 3,
    title: 'Canon EOS R50 Mirrorless Camera',
    category: 'Camera',
    image:
      'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&w=900&q=80',
    price: 799.0,
    oldPrice: 899.0,
    rating: 4.6,
    badge: 'New',
  },
  {
    id: 4,
    title: 'Logitech MX Mechanical Keyboard',
    category: 'Accessories',
    image:
      'https://images.unsplash.com/photo-1511467687858-23d96c32e4ae?auto=format&fit=crop&w=900&q=80',
    price: 159.99,
    oldPrice: 189.99,
    rating: 4.5,
    badge: '',
  },
  {
    id: 5,
    title: 'Logitech MX Mechanical Keyboard',
    category: 'Accessories',
    image:
      'https://images.unsplash.com/photo-1511467687858-23d96c32e4ae?auto=format&fit=crop&w=900&q=80',
    price: 159.99,
    oldPrice: 189.99,
    rating: 4.5,
    badge: '',
  },
]

const [emblaRef, emblaApi] = emblaCarouselVue({
  loop: false,
  align: 'start',
  slidesToScroll: 1,
})

const canScrollPrev = ref(false)
const canScrollNext = ref(true)

function updateScrollState() {
  if (!emblaApi.value) return
  canScrollPrev.value = emblaApi.value.canScrollPrev()
  canScrollNext.value = emblaApi.value.canScrollNext()
}

function scrollPrev() {
  emblaApi.value?.scrollPrev()
}

function scrollNext() {
  emblaApi.value?.scrollNext()
}

onMounted(() => {
  setTimeout(() => {
    updateScrollState()
    emblaApi.value?.on('select', updateScrollState)
    emblaApi.value?.on('reInit', updateScrollState)
  }, 0)
})

onBeforeUnmount(() => {
  emblaApi.value?.destroy()
})
</script>
