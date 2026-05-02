<template>
  <section class="">
    <HeroSection />
    <Categories />
    <FeatureProduct />
    <TrandingProduct />
    <SpecialOfferBanner />
  </section>
</template>

<script setup>
import TrandingProduct from '@/components/home/TrandingProduct.vue'
import Categories from '../components/home/Categories.vue'
import FeatureProduct from '../components/home/FeatureProduct.vue'
import HeroSection from '../components/home/HeroSection.vue'
import SpecialOfferBanner from '../components/home/SpecialOfferBanner.vue'
</script>
