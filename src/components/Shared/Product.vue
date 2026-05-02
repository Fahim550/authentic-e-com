<template>
  <article
    class="group flex cursor-pointer flex-col overflow-hidden rounded-2xl border border-gray-200 bg-white shadow-sm transition hover:-translate-y-1 hover:shadow-md"
  >
    <div class="relative overflow-hidden bg-gray-50">
      <span
        v-if="badge"
        class="absolute left-3 top-3 z-10 rounded-full bg-primary px-3 py-1 text-xs font-semibold text-white"
      >
        {{ badge }}
      </span>

      <img
        :src="image"
        :alt="title"
        class="h-64 w-full object-cover transition duration-300 group-hover:scale-105"
        loading="lazy"
      />

      <div
        class="absolute right-3 top-1/3 z-10 flex -translate-y-1/2 translate-x-10 flex-col gap-2 opacity-0 transition duration-300 group-hover:translate-x-0 group-hover:opacity-100"
      >
        <Tooltip text="Wishlist" placement="left">
          <button
            type="button"
            class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow hover:bg-primary hover:text-white cursor-pointer"
            aria-label="Add to wishlist"
          >
            <!-- title="Wishlist" -->
            <Heart class="h-6 w-6" />
          </button>
        </Tooltip>

        <Tooltip text="Quick view" placement="left">
          <button
            class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow hover:bg-primary hover:text-white cursor-pointer"
            aria-label="Quick View"
          >
            <!-- title="Quick View" -->
            <Eye class="h-6 w-6" />
          </button>
        </Tooltip>

        <Tooltip text="Compare" placement="left">
          <button
            type="button"
            class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow hover:bg-primary hover:text-white cursor-pointer"
            aria-label="Compare"
          >
            <!-- title="Compare" -->
            <GitCompareArrows class="h-6 w-6" />
          </button>
        </Tooltip>
      </div>
    </div>

    <div class="flex flex-1 flex-col p-4">
      <p class="text-xs font-medium uppercase tracking-wide text-gray-500">{{ category }}</p>
      <h3 class="mt-1 line-clamp-2 text-base font-semibold text-primary">{{ title }}</h3>

      <div class="mt-2 flex items-center gap-1 text-sm">
        <Star
          v-for="starIndex in 5"
          :key="starIndex"
          class="h-4 w-4"
          :class="starIndex <= normalizedRating ? 'text-amber-500' : 'text-gray-300'"
          :fill="starIndex <= normalizedRating ? 'currentColor' : 'none'"
        />
        <span class="ml-1 text-xs text-gray-500">({{ normalizedRating.toFixed(1) }})</span>
      </div>

      <div class="mt-4 relative h-10 overflow-hidden">
        <div
          class="absolute inset-0 flex items-center gap-2 transition duration-300 group-hover:-translate-x-full group-hover:opacity-0"
        >
          <span class="text-lg font-bold text-primary">${{ price.toFixed(2) }}</span>
          <span v-if="oldPrice" class="text-sm text-accent/80 line-through"
            >${{ oldPrice.toFixed(2) }}</span
          >
        </div>

        <button
          type="button"
          class="absolute inset-y-0 left-0 flex -translate-x-full items-center gap-2 text-sm font-semibold text-accent transition duration-300 group-hover:translate-x-0 cursor-pointer"
        >
          <ShoppingCart class="h-6 w-6" />
          Add to cart
        </button>
      </div>
    </div>
  </article>
</template>

<script setup>
import Tooltip from '@/ui/Tooltip.vue'
import { Eye, GitCompareArrows, Heart, ShoppingCart, Star } from '@lucide/vue'
import { computed } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  category: {
    type: String,
    default: 'Product',
  },
  image: {
    type: String,
    required: true,
  },
  price: {
    type: Number,
    required: true,
  },
  oldPrice: {
    type: Number,
    default: null,
  },
  rating: {
    type: Number,
    default: 4.5,
  },
  badge: {
    type: String,
    default: '',
  },
})

const normalizedRating = computed(() => Math.max(0, Math.min(5, props.rating)))
</script>
