<template>
  <section class="space-y-5">
    <HeroSection />
    <Categories />
    <FeatureProduct />
    <TrandingProduct />
  </section>
</template>

<script setup>
import HeroSection from '../components/home/HeroSection.vue'
import Categories from '../components/home/Categories.vue'
import FeatureProduct from '../components/home/FeatureProduct.vue'
import TrandingProduct from '@/components/home/TrandingProduct.vue'
</script>
