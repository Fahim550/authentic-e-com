<template>
  <section class="rounded-2xl bg-white mx-auto p-4 sm:p-20 w-full">
    <h2 class="text-center text-xl font-bold text-[#17172b] sm:text-2xl">Featured Categories</h2>

    <div class="mt-4 pt-10 flex gap-5 overflow-x-auto pb-2 sm:grid sm:grid-cols-3 sm:gap-6 sm:overflow-visible md:grid-cols-4 lg:grid-cols-6">
      <article
        v-for="category in categories"
        :key="category.name"
        class="min-w-[104px] sm:min-w-0 flex flex-col items-center text-center cursor-pointer"
      >
        <div
          class="mx-auto flex h-24 w-24 items-center justify-center rounded-full border border-gray-200 bg-white p-3 shadow-sm transition hover:-translate-y-1 hover:shadow-md"
        >
          <img
            :src="category.image"
            :alt="category.name"
            class="h-14 w-14 object-contain"
            loading="lazy"
          />
        </div>
        <p class="pt-3 text-sm font-medium text-gray-800">{{ category.name }}</p>
      </article>
    </div>
  </section>
</template>

<script setup>
const categories = [
  {
    name: 'Headphones',
    image: 'https://cdn-icons-png.flaticon.com/512/3659/3659898.png',
  },
  {
    name: 'Fashion',
    image: 'https://cdn-icons-png.flaticon.com/512/892/892458.png',
  },
  {
    name: 'Mobile & Tablets',
    image: 'https://cdn-icons-png.flaticon.com/512/545/545245.png',
  },
  {
    name: 'Cosmetics',
    image: 'https://cdn-icons-png.flaticon.com/512/3163/3163202.png',
  },
  {
    name: 'Furniture',
    image: 'https://cdn-icons-png.flaticon.com/512/1465/1465922.png',
  },
  {
    name: 'Handbags',
    image: 'https://cdn-icons-png.flaticon.com/512/2331/2331966.png',
  },
];
</script>