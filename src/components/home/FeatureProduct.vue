<template>
  <section class="mx-auto w-full rounded-2xl bg-white px-4 py-10 sm:px-6 lg:px-14">
    <div class="flex flex-wrap items-end justify-between gap-3">
      <div>
        <p class="text-sm font-semibold uppercase tracking-wider text-gray-500">Curated Picks</p>
        <h2 class="mt-1 text-2xl font-bold text-[#17172b] sm:text-3xl">Featured Products</h2>
      </div>
      <a href="#" class="text-sm font-semibold text-[#17172b] hover:underline">View all products</a>
    </div>

    <div class="mt-8 grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-4">
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
      />
    </div>
  </section>
</template>

<script setup>
import Product from '../Shared/Product.vue';

const featuredProducts = [
  {
    id: 1,
    title: 'Sony WH-1000XM5 Wireless Headphones',
    category: 'Audio',
    image: 'https://images.unsplash.com/photo-1546435770-a3e426bf472b?auto=format&fit=crop&w=900&q=80',
    price: 339.99,
    oldPrice: 399.99,
    rating: 4.8,
    badge: '20% OFF',
  },
  {
    id: 2,
    title: 'Apple Watch Series 9 GPS 45mm',
    category: 'Wearables',
    image: 'https://images.unsplash.com/photo-1546868871-7041f2a55e12?auto=format&fit=crop&w=900&q=80',
    price: 429.0,
    oldPrice: 499.0,
    rating: 4.7,
    badge: 'Hot',
  },
  {
    id: 3,
    title: 'Canon EOS R50 Mirrorless Camera',
    category: 'Camera',
    image: 'https://images.unsplash.com/photo-1516035069371-29a1b244cc32?auto=format&fit=crop&w=900&q=80',
    price: 799.0,
    oldPrice: 899.0,
    rating: 4.6,
    badge: 'New',
  },
  {
    id: 4,
    title: 'Logitech MX Mechanical Keyboard',
    category: 'Accessories',
    image: 'https://images.unsplash.com/photo-1511467687858-23d96c32e4ae?auto=format&fit=crop&w=900&q=80',
    price: 159.99,
    oldPrice: 189.99,
    rating: 4.5,
    badge: '',
  },
];
</script>