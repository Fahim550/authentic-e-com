<template>
  <article
    class="group flex flex-col overflow-hidden rounded-2xl border border-gray-200 bg-white shadow-sm transition hover:-translate-y-1 hover:shadow-md"
  >
    <div class="relative overflow-hidden bg-gray-50">
      <span
        v-if="badge"
        class="absolute left-3 top-3 z-10 rounded-full bg-[#17172b] px-3 py-1 text-xs font-semibold text-white"
      >
        {{ badge }}
      </span>

      <img
        :src="image"
        :alt="title"
        class="h-56 w-full object-cover transition duration-300 group-hover:scale-105"
        loading="lazy"
      />

      <div
        class="absolute right-3 top-1/2 z-10 flex -translate-y-1/2 translate-x-10 flex-col gap-2 opacity-0 transition duration-300 group-hover:translate-x-0 group-hover:opacity-100"
      >
        <button
          type="button"
          class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow-sm transition hover:bg-[#17172b] hover:text-white"
          aria-label="Add to wishlist"
        >
          <Heart class="h-4 w-4" />
        </button>

        <button
          type="button"
          class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow-sm transition hover:bg-[#17172b] hover:text-white"
          aria-label="Quick view"
        >
          <Eye class="h-4 w-4" />
        </button>

        <button
          type="button"
          class="flex h-9 w-9 items-center justify-center rounded-lg bg-white text-gray-600 shadow-sm transition hover:bg-[#17172b] hover:text-white"
          aria-label="Compare"
        >
          <GitCompareArrows class="h-4 w-4" />
        </button>
      </div>
    </div>

    <div class="flex flex-1 flex-col p-4">
      <p class="text-xs font-medium uppercase tracking-wide text-gray-500">{{ category }}</p>
      <h3 class="mt-1 line-clamp-2 text-base font-semibold text-[#17172b]">{{ title }}</h3>

      <div class="mt-2 flex items-center gap-1 text-sm text-amber-500">
        <span v-for="starIndex in 5" :key="starIndex">
          {{ starIndex <= normalizedRating ? '★' : '☆' }}
        </span>
        <span class="ml-1 text-xs text-gray-500">({{ normalizedRating.toFixed(1) }})</span>
      </div>

      <div class="mt-4 relative h-10 overflow-hidden">
        <div
          class="absolute inset-0 flex items-center gap-2 transition duration-300 group-hover:-translate-x-full group-hover:opacity-0"
        >
          <span class="text-lg font-bold text-[#17172b]">${{ price.toFixed(2) }}</span>
          <span v-if="oldPrice" class="text-sm text-gray-400 line-through">${{ oldPrice.toFixed(2) }}</span>
        </div>

        <button
          type="button"
          class="absolute inset-y-0 left-0 flex -translate-x-full items-center text-sm font-semibold text-[#df1a49] transition duration-300 group-hover:translate-x-0"
        >
          Add to cart
        </button>
      </div>
    </div>
  </article>
</template>

<script setup>
import { computed } from 'vue';
import { Eye, GitCompareArrows, Heart } from '@lucide/vue';

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
});

const normalizedRating = computed(() => Math.max(0, Math.min(5, props.rating)));
</script>